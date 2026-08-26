---
name: score-location-business-interruption
description: >-
  Score the business-interruption (downtime) risk of a single physical location with the One
  Concern Domino AI API, choosing the right operation for the question being asked and handling
  the coverage and enum traps that cause most failures.
api: One Concern Domino AI API
base_url: https://api.oneconcern.com
spec: openapi/one-concern-domino-ai-openapi.json
operations:
  - Business_Interruption_Risk_Scores_By_Return_Period_v1_location_business_interruption_return_period_post
  - Business_Interruption_Risk_Scores_By_Average_Annual_Downtime_v1_location_business_interruption_average_annual_post
  - BI_Risk_Score_By_Planning_Horizon_v1_location_business_interruption_planning_horizon_post
generated: '2026-08-26'
method: generated
source: >-
  openapi/one-concern-domino-ai-openapi.json (v1.31.2),
  https://developer.oneconcern.com/overview, https://developer.oneconcern.com/calculation-process
---

# Score a location's business-interruption risk

The Domino AI API answers one question: if a catastrophe of a given severity hits this
coordinate, how many days is the business at that location down — counting not just damage to
the building but disruption to the power, ports, roads and community it depends on.

## Before you start

You need a One Concern API token. There is no sign-up: tokens come from the customer success team
(see https://developer.oneconcern.com/overview). Your token may authorize only some of the five
operations even though the specification describes all of them.

Every request needs two headers beyond `Content-Type`:

- `x-1c-api-token` — your token.
- `client-id` — any value meaningful to you. It is required, it is not a credential, and One
  Concern uses it to break out your call volume for billing.
- `transaction-id` — optional, your own per-call identifier, echoed into billing reports.

## Step 1 — pick the operation that matches the question

| Question | Operation |
|---|---|
| "How bad is a 1-in-250-year flood here?" | `Business_Interruption_Risk_Scores_By_Return_Period_v1_location_business_interruption_return_period_post` — `POST /v1/location/business-interruption/return-period` |
| "What is the expected annual downtime here?" | `Business_Interruption_Risk_Scores_By_Average_Annual_Downtime_v1_location_business_interruption_average_annual_post` — `POST /v1/location/business-interruption/average-annual` |
| "What does this look like over the next 20 years?" | `BI_Risk_Score_By_Planning_Horizon_v1_location_business_interruption_planning_horizon_post` — `POST /v1/location/business-interruption/planning-horizon` |

Underwriting a single treaty at a stated exceedance probability uses the return-period operation.
Pricing an annual premium or benchmarking a portfolio uses average-annual. Capital planning and
disclosure use planning-horizon.

## Step 2 — build the request body

Common to all three:

- `latitude` (-90 to 90) and `longitude` (-180 to 180), required.
- `max_distance_m` — how far the model may look for a building, 1.0 to 500.0 metres, default 500.
- `interruption_type` — one of `integrated`, `utility`, `ingress_egress`, `community`,
  `repair_time`, `ports`, `airports`, `bridges`, `highways`. Use `integrated` unless you are
  specifically isolating one lifeline.
- `climate_change` — `ccbaseline` or `cc2050_45`.
- `peril` — see the trap below.

Then the operation-specific field: `return_period_yrs` (50, 100, 250, 500, 1000) or
`planning_horizon_yrs` (1, 5, 10, 20, 30). Average-annual takes neither.

### The peril trap

`peril` uses two different enumerations with the same field name:

- return-period operation: `flood`, `wind`, `seismic` only.
- average-annual and planning-horizon operations: `flood`, `wind`, `seismic`, **and**
  `integrated`.

Sending `peril: integrated` to the return-period operation returns 422 with a message naming the
permitted members. Do not share one enum across your three call sites.

## Step 3 — read the response

A 200 returns:

- `id` — One Concern's UUID for the building the model snapped to. It is the model's choice, not
  yours; two nearby coordinates can return the same id.
- `downtime_avg_days` and `downtime_stdev_days`.
- `score` — `low`, `med` or `high`. High is downtime >= 7 days, medium >= 2 and < 7, low < 2. For
  the average-annual operation the bins are applied to `downtime_avg_days + 2 *
  downtime_stdev_days`, not to the mean alone.

## Step 4 — handle 204 before you handle errors

**HTTP 204 No Content is a valid answer.** It means the request was well formed and authorized but
there is no modeled building within `max_distance_m` of the coordinate. The body is empty, so any
code that calls `.json()` on a 2xx will throw here.

Treat it as "outside modeled coverage" and report it as such. Widening `max_distance_m` up to the
500 m maximum may resolve it. Do not retry the identical request. Note also that One Concern warns
different countries and peril combinations support different dependencies — an accepted
`interruption_type` can still yield 204 for a given location.

## Step 5 — error handling

- `401` with `{"error": "Authorization field missing"}` — the token header is absent, invalid, or
  not entitled to this endpoint. One Concern directs you to customer success rather than a
  self-service fix, so do not loop.
- `422` with `{"detail": [{"loc": [...], "msg": "...", "type": "..."}]}` — a value is out of range
  or not a member of an enum. The `msg` names the permitted members; read it rather than guessing.
- `5xx` — rare, and safe to retry: the API is read-only.

See `errors/one-concern-problem-types.yml` for the full catalog.

## Step 6 — record the version headers

Every response carries `x-1c-api-version` (the code version) and `x-1c-data-version` (the dataset
version). One Concern explicitly recommends recording both for any use case that needs an audit
trail, because model improvements change the numbers without changing the endpoint and are
announced through customer success rather than a public changelog. If you are producing a figure
that will be defended later, store the pair alongside the result.

## Portfolio work

There is no batch or list operation. Scoring N locations is N requests. No rate limits are
published, and the gateway (Tyk) enforces limits set per contract that you cannot discover from
the API — pace conservatively and ask customer success for your quota before a bulk run.
