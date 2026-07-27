---
name: Harvest ERCOT 60-day SCED and DAM disclosure reports and historic archives
description: >-
  Pull ERCOT's 60-day disclosure reports — resource-level SCED and DAM offer, bid, award and
  telemetry data — and reach back past the API window using the historic archive endpoint.
api: openapi/ercot-public-data-api-openapi.json
base_url: https://api.ercot.com/api/public-reports
operations:
  - getData_33
  - getData_38
  - getData_41
  - getData_43
  - getData_45
  - getData_46
  - getData_47
  - getData_49
  - getData_51
  - getData_53
  - getData_55
  - getProductHistory
generated: '2026-07-27'
method: generated
source: openapi/ercot-public-data-api-openapi.json + https://developer.ercot.com/applications/pubapi/known-limits/
---

# Harvest ERCOT 60-day disclosures

Complete `ercot-authenticate-and-discover` first. This is the resource-level data — the richest and
the heaviest surface in the Public Data API. Plan for paging and the rate limit.

## 60-Day SCED disclosure (NP3-965-ER)

| What you want | Path | operationId |
|---|---|---|
| SCED generation resource data | `/np3-965-er/60_sced_gen_res_data` | `getData_53` |
| Load resource data in SCED | `/np3-965-er/60_load_res_data_in_sced` | `getData_55` |
| Settlement metered net energy for generation resources | `/np3-965-er/60_sced_smne_gen_res` | `getData_51` |
| QSE self-arranged AS in SCED | `/np3-965-er/60_sced_qse_self_arranged_as` | `getData_52` |
| HDL/LDL manual override summary | `/np3-965-er/60_hdl_ldl_man_override` | `getData_56` |

## 60-Day DAM disclosure (NP3-966-ER)

| What you want | Path | operationId |
|---|---|---|
| DAM generation resource data | `/np3-966-er/60_dam_gen_res_data` | `getData_45` |
| DAM generation resource AS offers | `/np3-966-er/60_dam_gen_res_as_offers` | `getData_46` |
| DAM load resource data | `/np3-966-er/60_dam_load_res_data` | `getData_43` |
| DAM energy bids | `/np3-966-er/60_dam_energy_bids` | `getData_49` |
| DAM energy-only offers | `/np3-966-er/60_dam_energy_only_offers` | `getData_47` |
| DAM PTP obligation bids | `/np3-966-er/60_dam_ptp_obl_bids` | `getData_41` |
| DAM QSE self-arranged AS | `/np3-966-er/60_dam_qse_self_as` | `getData_38` |

## 60-Day COP updates (NP3-991-EX)

`/np3-991-ex/60_cop_all_updates` — `getData_33`.

## Watch the deprecations

The RTC+B implementation (Market Notice PR447_RTC+B, effective 2025-12-05) retired several
disclosure endpoints. `/np3-965-er/60_sced_dsr_load_data` (`getData_54`) and the whole NP3-990-EX
60-Day SASM family (`getData_34`–`getData_37`) are on the timetable at
https://developer.ercot.com/applications/pubapi/deprecation-notices/ — check
`lifecycle/ercot-lifecycle.yml` before building on any of them. ERCOT does **not** emit `Sunset` or
`Deprecation` response headers, so a retired endpoint fails as a plain error with no warning.

## Filter and page

Disclosure products key on `deliveryDateFrom`/`deliveryDateTo` and often `hourEndingFrom`/
`hourEndingTo`; several accept `qseName` and `resourceName` to narrow to a single market
participant or unit. Always narrow before paging — these are the largest result sets in the API.

Set `size` high and loop `page` until `_meta.currentPage == _meta.totalPages`, sleeping ≥ 2 seconds
between calls (30 requests per minute is the ceiling).

## Reaching past the API window

API data begins at each product's activation date in the Public Data API system; see the release
notes for activation dates. Anything older is available only as historic files:

```
GET /archive/{emilId}          # getProductHistory
```

The response lists `archives[]` with `docId`, `friendlyName` and `postDatetime`, paged the same way.
**Downloads are capped at 1,000 files per batch**, so chunk long backfills by date. Files are
retained at least seven years.

## Handling

- All 106 operations are GET; nothing here mutates and there is no idempotency key.
- Data is resource-level and identifies market participants by QSE and resource name — handle it
  under the ERCOT Terms of Use (https://www.ercot.com/help/terms/data-portal).
- Column meaning comes from the `fields[]` dictionary in each response, not from a static schema:
  `data` is declared as an untyped object in the spec.
