---
name: compare-property-damage-scenarios
description: >-
  Compare direct structural property-damage ratios for a location across perils, return periods
  and climate scenarios with the One Concern Domino AI API, and combine them with the
  business-interruption view without conflating the two measures.
api: One Concern Domino AI API
base_url: https://api.oneconcern.com
spec: openapi/one-concern-domino-ai-openapi.json
operations:
  - Property_Damage_Ratio_By_Return_Period_v1_location_property_damage_return_period_post
  - Property_Damage_Ratio_By_Average_Annual_Downtime_v1_location_property_damage_average_annual_post
  - Business_Interruption_Risk_Scores_By_Return_Period_v1_location_business_interruption_return_period_post
generated: '2026-08-26'
method: generated
source: >-
  openapi/one-concern-domino-ai-openapi.json (v1.31.2),
  https://developer.oneconcern.com/overview, https://developer.oneconcern.com/calculation-process
---

# Compare property-damage scenarios for a location

Property damage and business interruption are two different products in the Domino AI API and
they answer different questions. Damage is what happens to the building. Interruption is how long
the business at that building stops, including because the power, the port or the road is out.
A location can have a low damage ratio and a high downtime score.

## Operations

- `Property_Damage_Ratio_By_Return_Period_v1_location_property_damage_return_period_post` —
  `POST /v1/location/property-damage/return-period`
- `Property_Damage_Ratio_By_Average_Annual_Downtime_v1_location_property_damage_average_annual_post` —
  `POST /v1/location/property-damage/average-annual`

Both take `latitude`, `longitude`, `max_distance_m`, `peril` and `climate_change`. Only the
return-period operation takes `return_period_yrs`.

Note the damage operations take **no** `interruption_type` — that field belongs to business
interruption only. Sending it is a 422.

## Step 1 — sweep the return periods

Hold `peril` and `climate_change` fixed and issue one request per value of `return_period_yrs`
in `[50, 100, 250, 500, 1000]`. That is five requests; there is no batch operation and no way to
ask for a curve in one call.

Remember `peril` on the return-period operation accepts `flood`, `wind`, `seismic` — **not**
`integrated`. To get an all-perils view you must use the average-annual operation, which does
accept `integrated`.

## Step 2 — sweep the climate scenarios

Repeat the sweep with `climate_change: ccbaseline` and again with `climate_change: cc2050_45`
(RCP 4.5 or equivalent SSP for a 2050 projection year). The delta between the two curves is the
climate-change signal for that location and peril.

## Step 3 — read the response

- `damage_ratio_avg` — the mean direct structural impact of the hazard on the location.
- `damage_ratio_stdev` — its standard deviation.
- `id` — the One Concern building UUID the model snapped to.

There is no `score` band on the damage response. The low/med/high bands documented on the
calculation-process page apply to downtime, not to damage — do not carry them across.

## Step 4 — join to the interruption view carefully

The `id` field is documented identically on both response types ("ID (uuid) of the location"), so
a damage result and an interruption result for the same coordinate will usually carry the same
building id. The contract does not guarantee it, and there is no operation that takes an `id` as
input — you cannot look a building up, and you cannot verify the join. Key your own records on
the coordinate you sent plus the id you got back, and confirm the ids match before presenting a
combined damage-and-downtime figure for "the same building".

## Step 5 — coverage and errors

- `204` — no modeled building within `max_distance_m`. Valid answer, empty body, do not retry
  unchanged. Widen `max_distance_m` up to 500 m or record the location as out of coverage.
- `401` — token missing or not entitled to this endpoint; contact One Concern customer success.
- `422` — enum or range violation; the `msg` in the `detail` array names the permitted values.

## Step 6 — pin the result

Record `x-1c-api-version` and `x-1c-data-version` from the response headers with every figure. A
damage curve is only comparable to another damage curve computed from the same data version, and
One Concern ships model improvements without changing the endpoints.
