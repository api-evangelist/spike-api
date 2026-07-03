# Spike (spike-api)

Spike (Spike Technologies) provides a unified health and wearables data API that connects an application to 500+ wearables, IoT devices, CGMs, EMRs, labs, and nutrition sources through a single integration - aggregating Apple Health, Garmin, Fitbit, Oura, Whoop, Dexcom, Withings, Polar, Suunto, Strava, and more. Developers authenticate end users with HMAC signatures, connect providers via hosted OAuth-style integration flows, then query normalized health data - sleep, workouts, time series metrics (heart rate, HRV, glucose, weight, SpO2, steps), daily and interval statistics, nutrition, and lab reports - over a REST API at `https://app-api.spikeapi.com/v3`, with outbound webhooks pushing record-change events. Spike also ships mobile SDKs (iOS, Android, Flutter, React Native), a Nutrition AI scanner, and an MCP layer for AI-ready health data.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/spike-api/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/spike-api/refs/heads/main/apis.yml)

## Tags

- Health Data
- Wearables
- Fitness
- Digital Health
- Data Aggregation
- HIPAA

## Timestamps

- **Created:** 2026-07-03
- **Modified:** 2026-07-03

## APIs

### Spike Authentication API

Authenticate an application's end users and mint a JWT access token. The application signs the application user ID with its secret using HMAC-SHA256 and exchanges the signature at `/auth/hmac` (also `/auth/client_token` and `/auth/pkcs1`); the returned Bearer token authorizes all subsequent requests.

- **Human URL:** [https://docs.spikeapi.com/api-docs/authentication](https://docs.spikeapi.com/api-docs/authentication)
- **Base URL:** `https://app-api.spikeapi.com/v3`

### Spike Provider Integrations API

Connect and disconnect a user's data providers. Initialize a hosted integration flow (`/providers/{provider_slug}/integration/init` and `/init_url`), receive the provider OAuth callback, and delete an existing integration. Providers include Garmin, Fitbit, Oura, Whoop, Dexcom, FreeStyle Libre, Withings, Polar, Suunto, Strava, Coros, Wahoo, Ultrahuman, Omron, Huawei, Google Fit, and Google Health Connect.

- **Human URL:** [https://docs.spikeapi.com/api-docs/provider_integration](https://docs.spikeapi.com/api-docs/provider_integration)
- **Base URL:** `https://app-api.spikeapi.com/v3`

### Spike Provider Records API

List and retrieve normalized provider records - the discrete health data samples ingested from a user's connected providers - via `/queries/provider_records`, `/queries/provider_records/{record_id}`, and the compatibility `POST /queries/provider_record`, filtered by time range, provider, and metric.

- **Human URL:** [https://docs.spikeapi.com/api-reference/query-provider-records-list](https://docs.spikeapi.com/api-reference/query-provider-records-list)
- **Base URL:** `https://app-api.spikeapi.com/v3`

### Spike Sleep API

Query normalized sleep sessions with stage breakdowns (awake, light, deep, REM), duration, and efficiency via `/queries/sleeps` and `/queries/sleeps/{sleep_id}`, unified across every connected provider.

- **Human URL:** [https://docs.spikeapi.com/api-reference/query-sleep-list](https://docs.spikeapi.com/api-reference/query-sleep-list)
- **Base URL:** `https://app-api.spikeapi.com/v3`

### Spike Workouts API

List and retrieve workouts / physical activities with per-activity metrics (duration, distance, calories, heart rate zones) via `/queries/workouts` and `/queries/workouts/{workout_id}`, normalized across the full activity-type matrix.

- **Human URL:** [https://docs.spikeapi.com/api-reference/query-workouts-list](https://docs.spikeapi.com/api-reference/query-workouts-list)
- **Base URL:** `https://app-api.spikeapi.com/v3`

### Spike Time Series API

Retrieve high-resolution time series for a specified metric via `/queries/timeseries`, `/queries/timeseries/samples`, and `/queries/timeseries/split` (split by provider source). Metrics include heart rate, resting heart rate, HRV (RMSSD and SDNN), glucose, weight, body fat, SpO2, breathing rate, steps, distance, and calories burned - the surface through which heart-rate, body/weight, and CGM/glucose data are delivered.

- **Human URL:** [https://docs.spikeapi.com/api-reference/query-timeseries](https://docs.spikeapi.com/api-reference/query-timeseries)
- **Base URL:** `https://app-api.spikeapi.com/v3`

### Spike Statistics API

Compute aggregated statistics for metrics over time - daily rollups (`/queries/statistics/daily`), arbitrary intervals (`/queries/statistics/interval`), and interpolation (`/queries/statistics/interpolation`) - for building dashboards, trends, and Health Insight scores from unified biometric data.

- **Human URL:** [https://docs.spikeapi.com/api-reference/query-statistics-daily](https://docs.spikeapi.com/api-reference/query-statistics-daily)
- **Base URL:** `https://app-api.spikeapi.com/v3`

### Spike Nutrition AI API

Create, analyze, and manage nutrition records. Analyze a food image (`/nutrition_records/image`), a nutrition-facts label (`/nutrition_records/ingredients/label`), or a free-text meal (`/nutrition_records/text`), log a manual record (`/nutrition_records/manual`), then list, get, modify, replace, or delete records across 29 nutritional fields.

- **Human URL:** [https://docs.spikeapi.com/nutrition-ai/overview](https://docs.spikeapi.com/nutrition-ai/overview)
- **Base URL:** `https://app-api.spikeapi.com/v3`

### Spike Lab Reports API

Upload lab report documents (base64) for AI extraction, then process, list, and retrieve structured biomarker results via `/lab_reports`, `/lab_reports/process`, and `/lab_reports/{lab_report_id}`.

- **Human URL:** [https://docs.spikeapi.com/lab-reports/overview](https://docs.spikeapi.com/lab-reports/overview)
- **Base URL:** `https://app-api.spikeapi.com/v3`

### Spike Users API

Retrieve the current authenticated user's information and connected providers (`/userinfo`), user properties (`/userproperties`), and application-level configuration and available providers (`/applicationinfo`).

- **Human URL:** [https://docs.spikeapi.com/api-reference/user-info](https://docs.spikeapi.com/api-reference/user-info)
- **Base URL:** `https://app-api.spikeapi.com/v3`

### Spike SDK Push API

Ingest on-device health data pushed from the Spike mobile SDKs. The SDK posts Apple Health, Android Health Connect, and Samsung Health samples (JSON and protobuf) via `/providers/apple/push`, `/providers/health_connect/push`, and `/providers/samsung_health_data/push/proto` for normalization into the same query surface.

- **Human URL:** [https://docs.spikeapi.com/api-docs/overview](https://docs.spikeapi.com/api-docs/overview)
- **Base URL:** `https://app-api.spikeapi.com/v3`

### Spike Webhooks API

Outbound webhook event delivery. After data updates, Spike POSTs a JSON array of events - `record_change`, `provider_integration_created`, and `provider_integration_deleted` - to a webhook URL configured in the admin console, HMAC-SHA256 signed via the `X-Body-Signature` header, with retries (up to 10) on non-200 responses. Delivery is outbound HTTP only; there is no public WebSocket or SSE surface.

- **Human URL:** [https://docs.spikeapi.com/api-docs/webhooks](https://docs.spikeapi.com/api-docs/webhooks)
- **Base URL:** `https://app-api.spikeapi.com/v3`

## Common Properties

- [GitHub Organization](https://github.com/Spike-API)
- [LinkedIn](https://www.linkedin.com/company/spike-api)
- [Website](https://www.spikeapi.com)
- [Documentation](https://docs.spikeapi.com)
- [Plans](plans/spike-api-plans-pricing.yml)
- [Rate Limits](rate-limits/spike-api-rate-limits.yml)
- [Fin Ops](finops/spike-api-finops.yml)

## Review

Does Spike expose a documented public WebSocket API? **No.** Spike's public surface is a REST API at `https://app-api.spikeapi.com/v3` (Bearer JWT) plus outbound HMAC-signed webhooks. No WebSocket or SSE endpoint is documented. See [review.yml](review.yml).

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
