---
name: Authenticate to the ERCOT Public Data API and discover data products
description: >-
  Mint the two credentials every ERCOT Public Data API call requires (an Azure APIM subscription key
  and an hourly Azure AD B2C ID token), then walk the EMIL product catalog to find the report
  endpoint you actually need.
api: openapi/ercot-public-data-api-openapi.json
base_url: https://api.ercot.com/api/public-reports
operations:
  - getListForProducts
  - getProduct
  - getVersion
generated: '2026-07-27'
method: generated
source: >-
  https://developer.ercot.com/applications/pubapi/user-guide/registration-and-authentication/,
  https://developer.ercot.com/applications/pubapi/user-guide/using-api/,
  openapi/ercot-public-data-api-openapi.json
---

# Authenticate and discover ERCOT data products

This is the prerequisite for every other ERCOT skill. Do it first; nothing else works without it.

## 1. One-time setup (human, not agent)

Registration is free and self-serve but requires a browser and an email round-trip, so it cannot be
automated:

1. Go to https://apiexplorer.ercot.com/ and sign up with an email address; enter the emailed
   verification code, then set a password and display name.
2. Open the **Products** page, subscribe to the Public Data API product, and copy the **Primary
   key** from your profile. This is your `Ocp-Apim-Subscription-Key` and it does not expire.

Store the username, password and subscription key as secrets. The password is used directly against
the token endpoint (a legacy ROPC OAuth grant), so treat it accordingly.

## 2. Mint an ID token (every hour)

```
POST https://ercotb2c.b2clogin.com/ercotb2c.onmicrosoft.com/B2C_1_PUBAPI-ROPC-FLOW/oauth2/v2.0/token
Content-Type: application/x-www-form-urlencoded

username=<username>&password=<password>&grant_type=password
&scope=openid+fec253ea-0d06-4272-a5e6-b478baeecd70+offline_access
&client_id=fec253ea-0d06-4272-a5e6-b478baeecd70&response_type=id_token
```

Use the `id_token` from the response — not the `access_token`. It is valid for **3600 seconds and
cannot be refreshed**; when it expires, POST again. A `refresh_token` is returned but ERCOT's own
documentation states there is no refresh path for the ID token.

## 3. Call the API with BOTH credentials

Every request carries two headers:

```
Ocp-Apim-Subscription-Key: <subscription key>
Authorization: Bearer <id_token>
```

Omitting either yields a rejection (an anonymous call to the base URL returns 401). The subscription
key may alternatively be passed as a `subscription-key` query parameter, but the header is
preferred — do not put credentials in URLs you log.

## 4. Discover products — `getListForProducts`

`GET /` returns every available EMIL data product under `_embedded.products`. Each product carries
its `emilId` (e.g. `NP4-190-CD`), `name`, `description`, `generationFrequency`
(e.g. `Chron - Hourly`), `lastPostDatetime`, `archiveDuration` and an `artifacts[]` array. Each
artifact's `_links.endpoint.href` is the live report URL to call.

Use `generationFrequency` and `lastPostDatetime` to set your polling cadence — there are no
webhooks, and polling faster than the data posts just burns your rate limit.

## 5. Inspect one product — `getProduct`

`GET /{emilId}` (lower-cased in the path, e.g. `/np4-190-cd`) returns a single product with its
artifacts and `_links` for `self`, `parent` and `archive`. Follow `_links.archive.href` to reach
`getProductHistory` for files older than the product's API activation date.

## 6. Check the running version — `getVersion`

`GET /version` returns `info.title`, `info.description`, `info.version`, `info.build` and the
`openapi` version. Log it alongside any harvested dataset so results stay reproducible against a
release.

## Rules an agent must not break

- **30 requests per minute**, roughly one every two seconds. Exceeding it returns `429` with
  `{"error_key": "throttled", "error_message": "Too Many Requests"}`. No `Retry-After` header is
  published, so back off on a fixed schedule.
- **Non-US traffic is blocked** at the edge for all `*.ercot.com` hosts. A connection failure from
  outside the United States is expected behaviour, not a bug.
- Errors on `400`/`403`/`404` use the flat `Exception` envelope
  (`timestamp`, `code`, `status`, `message`, `data`) — **not** RFC 9457 problem+json. Gateway errors
  (`401`, `429`) use a different `error_key`/`error_message` shape. Handle both.
- The API is entirely read-only. There is no write operation, and therefore no idempotency key.

## Related

- `authentication/ercot-authentication.yml` — the full credential profile
- `conventions/ercot-conventions.yml` — paging, filtering and error conventions
- `rate-limits/ercot-rate-limits.yml` — the published limits
