---
name: Track ERCOT system load, wind and solar production, and outage capacity
description: >-
  Build a grid-conditions view from the ERCOT Public Data API — actual system load by weather and
  forecast zone, seven-day load forecasts, wind and solar actuals and forecasts (system-wide and by
  geographic region), and hourly resource outage capacity.
api: openapi/ercot-public-data-api-openapi.json
base_url: https://api.ercot.com/api/public-reports
operations:
  - getData_5
  - getData_6
  - getData_8
  - getData_9
  - getData_10
  - getData_11
  - getData_12
  - getData_13
  - getData_14
  - getData_15
  - getData_99
  - getData_100
  - getData_101
generated: '2026-07-27'
method: generated
source: openapi/ercot-public-data-api-openapi.json + https://www.ercot.com/mp/data-products
---

# Track ERCOT load, renewables and outages

Complete `ercot-authenticate-and-discover` first.

## Endpoints

Load — actual and forecast:

| What you want | Path | operationId |
|---|---|---|
| Actual system load by weather zone | `/np6-345-cd/act_sys_load_by_wzn` | `getData_6` |
| Actual system load by forecast zone | `/np6-346-cd/act_sys_load_by_fzn` | `getData_5` |
| Seven-day load forecast by model and weather zone | `/np3-565-cd/lf_by_model_weather_zone` | `getData_100` |
| Seven-day load forecast by model and study area | `/np3-566-cd/lf_by_model_study_area` | `getData_99` |

Wind:

| What you want | Path | operationId |
|---|---|---|
| Hourly averaged actual and forecast, system-wide | `/np4-732-cd/wpp_hrly_avrg_actl_fcast` | `getData_15` |
| Actual 5-minute averaged values | `/np4-733-cd/wpp_actual_5min_avg_values` | `getData_14` |
| Hourly actual and forecast by geographic region | `/np4-742-cd/wpp_hrly_actual_fcast_geo` | `getData_11` |
| Actual 5-minute averaged by geographic region | `/np4-743-cd/wpp_actual_5min_avg_values_geo` | `getData_10` |

Solar:

| What you want | Path | operationId |
|---|---|---|
| Hourly averaged actual and forecast, system-wide | `/np4-737-cd/spp_hrly_avrg_actl_fcast` | `getData_13` |
| Actual 5-minute averaged values | `/np4-738-cd/spp_actual_5min_avg_values` | `getData_12` |
| Hourly actual and forecast by geographic region | `/np4-745-cd/spp_hrly_actual_fcast_geo` | `getData_9` |
| Actual 5-minute averaged by geographic region | `/np4-746-cd/spp_actual_5min_avg_values_geo` | `getData_8` |

Supply availability:

| What you want | Path | operationId |
|---|---|---|
| Hourly resource outage capacity | `/np3-233-cd/hourly_res_outage_cap` | `getData_101` |

## Filter and page

These products are keyed on `deliveryDateFrom`/`deliveryDateTo` and `hourEndingFrom`/`hourEndingTo`;
the 5-minute products add `intervalEndingFrom`/`intervalEndingTo`. All accept `page`, `size`,
`sort`, `dir` and return `_meta.totalPages`. Resolve columns from the `fields[]` dictionary rather
than by position.

## Interpretation rules that matter

- **Wind and solar forecasts predict HSL — uncurtailed potential — while the actuals are affected by
  curtailment.** ERCOT states in the NP4-732-CD product description that this report should not be
  used to evaluate forecast performance. Do not compute forecast error from actual vs. forecast in
  these products and present it as ERCOT's forecast skill.
- The hourly wind/solar products carry a rolling 48-hour history plus a rolling 168-hour forward
  horizon, so each poll overwrites overlapping windows — upsert on (delivery date, hour ending,
  DSTFlag, region), do not append.
- NP3-233-CD outage capacity aggregates ACTIVE outages from the Outage Scheduler for the next 168
  hours, excluding retirements, mothballed and seasonal-mothballed units. It reflects the scheduler,
  not telemetry, and includes de-rates as well as full outages.

## Cadence

Read `generationFrequency` and `lastPostDatetime` from `getProduct` for each EMIL id and poll just
after the posting interval. There is no webhook or streaming option for public consumers, and the
rate limit is 30 requests per minute across everything you do.

## DST

`DSTFlag` and `repeatHourFlag` disambiguate the repeated fall-back hour. Include them in the primary
key of any time series you persist.
