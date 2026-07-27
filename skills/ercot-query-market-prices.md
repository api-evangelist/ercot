---
name: Query ERCOT day-ahead and real-time market prices
description: >-
  Pull settlement point prices, locational marginal prices, shadow prices and system lambda from the
  ERCOT Public Data API for both the Day-Ahead and Real-Time markets, paging correctly and handling
  the daylight-saving repeated hour.
api: openapi/ercot-public-data-api-openapi.json
base_url: https://api.ercot.com/api/public-reports
operations:
  - getData
  - getData_1
  - getData_2
  - getData_3
  - getData_4
  - getData_7
  - getData_16
  - getData_27
  - getData_28
  - getData_29
  - getData_30
generated: '2026-07-27'
method: generated
source: openapi/ercot-public-data-api-openapi.json + https://developer.ercot.com/applications/pubapi/user-guide/using-api/
---

# Query ERCOT market prices

Complete `ercot-authenticate-and-discover` first — both credentials are required here.

## Pick the right endpoint

Day-Ahead Market:

| What you want | Path | operationId |
|---|---|---|
| DAM settlement point prices | `/np4-190-cd/dam_stlmnt_pnt_prices` | `getData_28` |
| DAM hourly LMPs | `/np4-183-cd/dam_hourly_lmp` | `getData_30` |
| DAM clearing prices for capacity (AS MCPCs) | `/np4-188-cd/dam_clear_price_for_cap` | `getData_29` |
| DAM shadow prices | `/np4-191-cd/dam_shadow_prices` | `getData_27` |
| DAM system lambda | `/np4-523-cd/dam_system_lambda` | `getData_16` |

Real-Time Market:

| What you want | Path | operationId |
|---|---|---|
| Settlement point prices at nodes, hubs, load zones | `/np6-905-cd/spp_node_zone_hub` | `getData_1` |
| LMPs by resource node, load zone, trading hub | `/np6-788-cd/lmp_node_zone_hub` | `getData_3` |
| LMP by electrical bus | `/np6-787-cd/lmp_electrical_bus` | `getData_4` |
| RTD indicative LMPs | `/np6-970-cd/rtd_lmp_node_zone_hub` | `getData` |
| SCED shadow prices and binding transmission constraints | `/np6-86-cd/shdw_prices_bnd_trns_const` | `getData_2` |
| SCED system lambda | `/np6-322-cd/sced_system_lambda` | `getData_7` |

If you need something not listed, call `getListForProducts` (`GET /`) and read
`artifacts[]._links.endpoint.href` — do not guess a path.

## Filter

Day-ahead products are keyed on delivery date and hour:

```
GET /np4-190-cd/dam_stlmnt_pnt_prices?deliveryDateFrom=2026-07-01&deliveryDateTo=2026-07-07
    &settlementPoint=HB_NORTH&size=1000&page=1
```

Real-time SCED products are keyed on the SCED timestamp:

```
GET /np6-905-cd/spp_node_zone_hub?SCEDTimestampFrom=2026-07-01T00:00:00&SCEDTimestampTo=2026-07-01T23:59:59
```

Range filters follow a strict `<field>From` / `<field>To` convention. Which columns are filterable is
not guesswork: every response returns a `fields[]` dictionary with `searchable`, `sortable` and
`hasRange` per column. Read it once per product and cache it.

## Page

All price endpoints take `page`, `size`, `sort` and `dir`. The response `_meta` block returns
`totalRecords`, `pageSize`, `totalPages` and `currentPage`. Loop until `currentPage == totalPages`,
sleeping at least two seconds between calls to stay under 30 requests per minute.

## Read the payload

Responses are column-oriented: `fields[]` describes the columns, `data` carries the rows,
`report` identifies the source report (`reportName`, `reportDisplayName`, `reportId`, `reportEMIL`).
Do not hard-code column positions across releases — resolve them from `fields[]` by name each run.

## Handle the repeated hour

Market time is **America/Chicago**. At the autumn DST transition the same hour ending occurs twice.
`DSTFlag` and `repeatHourFlag` disambiguate it, and both appear as query parameters and as columns.
A price series keyed only on (date, hourEnding) will silently collide one hour a year — include the
flag in the key.

## Corrections matter

ERCOT restates prices. Before treating a settled price as final, check the corrections products:
`/np4-196-m/dam_price_corrections_spp` (`getData_24`) and
`/np4-197-m/rtm_price_corrections_spp` (`getData_18`), plus their EBLMP, SOG and shadow-price
siblings. A pipeline that never reads the `-M` products will drift from ERCOT settlement.

## Going back in time

The API serves data from each product's activation date forward. Older data is in the archive:
`GET /archive/{emilId}` (`getProductHistory`) lists zip files retained at least seven years, capped
at 1,000 files per download.
