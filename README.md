# ERCOT (ercot)

The Electric Reliability Council of Texas (ERCOT) is the independent system operator that manages the flow of electric power to roughly 27 million Texas customers on the ERCOT Interconnection, running the wholesale Day-Ahead and Real-Time energy markets, ancillary services, congestion revenue rights, and retail switching for the competitive Texas market. Its home market is the United States (Texas). ERCOT sits at the wholesale/system-operator layer of the energy value chain, upstream of the transmission and distribution utilities (Oncor, CenterPoint, AEP Texas, TNMP) and the retail electric providers that serve end customers. Its API posture is a clean split: market and grid data are genuinely open — ERCOT publishes a real, versioned OpenAPI 3.0 for the Public Data API covering 106 EMIL data-product endpoints (locational marginal prices, settlement point prices, system load, wind and solar production, ancillary services, outage capacity), and the Market Information System still serves public report archives anonymously with no account at all. Consumer energy data is a different story: ERCOT operates no consumer usage API and implements no Green Button / ESPI surface. Texas residential interval data lives in Smart Meter Texas, which is operated by the joint Transmission and Distribution Utilities under PUCT oversight, not by ERCOT. The market-participant SOAP estate (ERCOT Web Services, MarkeTrak, Retail API) is documented publicly on GitHub but reachable only by certified market participants.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/ercot/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/ercot/refs/heads/main/apis.yml)

## Tags

- Energy
- United States
- Electricity
- Energy Markets
- Grid
- System Operator
- Texas
- Renewables
- Demand Response
- Open Data

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### ERCOT Public Data API

RESTful access to ERCOT Market Information List (EMIL) public data products — 106 documented endpoints spanning real-time and day-ahead locational marginal prices, settlement point prices, SCED system lambda and shadow prices, actual system load by weather and forecast zone, wind and solar power production actuals and forecasts, ancillary service offers and awards, hourly resource outage capacity, and 60-day SCED/DAM disclosure reports, plus historic file archives retained at least seven years. Data is public and free, but every call requires a free self-serve Azure API Management subscription key plus an Azure AD B2C ID token. Rate limited to 30 requests per minute; requests from outside the United States are blocked.

- **Human URL:** [https://developer.ercot.com/applications/pubapi/user-guide/using-api/](https://developer.ercot.com/applications/pubapi/user-guide/using-api/)
- **Base URL:** `https://api.ercot.com/api/public-reports`

#### Tags

- Energy Markets
- Electricity
- Pricing
- Load
- Renewables
- Open Data

#### Properties

- [OpenAPI](openapi/ercot-public-data-api-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://developer.ercot.com/applications/pubapi/user-guide/using-api/)
- [API Reference](https://apiexplorer.ercot.com/api-details#api=pubapi-apim-api)
- [Authentication](https://developer.ercot.com/applications/pubapi/user-guide/registration-and-authentication/)
- [Rate Limits](https://developer.ercot.com/applications/pubapi/known-limits/)
- [Change Log](https://developer.ercot.com/applications/pubapi/relnotes/)
- [Deprecation](https://developer.ercot.com/applications/pubapi/deprecation-notices/)
- [OpenID Configuration](https://ercotb2c.b2clogin.com/ercotb2c.onmicrosoft.com/B2C_1_PUBAPI-ROPC-FLOW/v2.0/.well-known/openid-configuration)

### ERCOT ESR Public Data API

Energy Storage Resource public data, launched May 29, 2025 per the ERCOT Public Data API release notes, beginning with four-second ESR charging MW telemetry (`GET /rptesr-m/4_sec_esr_charging_mw`). Documented in the ERCOT API Explorer as the `esrapi-apim-api` product. No machine-readable specification is published for this API in ERCOT's public api-specs repository, and no base URL was independently confirmed, so none is asserted here. Access follows the same subscription-key plus B2C ID token model as the Public Data API.

- **Human URL:** [https://apiexplorer.ercot.com/api-details#api=esrapi-apim-api](https://apiexplorer.ercot.com/api-details#api=esrapi-apim-api)

#### Tags

- Energy Storage
- Batteries
- Telemetry
- Energy Markets

#### Properties

- [API Reference](https://apiexplorer.ercot.com/api-details#api=esrapi-apim-api)
- [Change Log](https://developer.ercot.com/applications/pubapi/relnotes/)
- [Authentication](https://developer.ercot.com/applications/pubapi/user-guide/registration-and-authentication/)

### ERCOT Web Services (EWS)

ERCOT's SOAP web-services estate for Nodal market participants — the Market Information Service, Market Transaction Service (bid and offer submission via BidSet), Resource Parameter Transaction Service, Outage Scheduling Services, Verbal Dispatch Instructions, and WS-Notifications callbacks. WSDL and XSD contracts are published openly on GitHub, but the runtime endpoints are reachable only by registered ERCOT Market Participants holding an ERCOT digital certificate; the shipped WSDL carries a placeholder `soap:address` of `https://dummyhost:0000/` so no runtime base URL is asserted here.

- **Human URL:** [https://developer.ercot.com/applications/ews/Introduction/](https://developer.ercot.com/applications/ews/Introduction/)

#### Tags

- SOAP
- Market Participants
- Bids
- Outages
- Energy Markets

#### Properties

- [WSDL](https://raw.githubusercontent.com/ercot/api-specs/main/ews/wsdls/Nodal.wsdl)
- [WSDL](https://raw.githubusercontent.com/ercot/api-specs/main/ews/wsdls/Notification.wsdl)
- [Documentation](https://developer.ercot.com/applications/ews/Introduction/)
- [Documentation](https://developer.ercot.com/applications/ews/Services%20Organization/)
- [Source Code](https://github.com/ercot/ews-client)

### ERCOT MarkeTrak API

SOAP API over MarkeTrak, ERCOT's retail-market issue tracking system, supporting QueryList, QueryDetail, Update, and Submit operations against retail transaction issues. Applications must pass ERCOT certification at one of three levels before they may call the service in production, and access is limited to registered Market Participants.

- **Human URL:** [https://developer.ercot.com/applications/marketrak/MarkeTrak_API_Dev_v1_2/](https://developer.ercot.com/applications/marketrak/MarkeTrak_API_Dev_v1_2/)
- **Base URL:** `https://misapi.ercot.com/marketrakAPI/`

#### Tags

- SOAP
- Retail
- Market Participants
- Issue Tracking

#### Properties

- [WSDL](https://raw.githubusercontent.com/ercot/api-specs/main/marketrak/MarkeTrakAPI_rc5_v14.wsdl)
- [Schema](https://raw.githubusercontent.com/ercot/api-specs/main/marketrak/MarkeTrakAPI_rc5_v14.xsd)
- [Documentation](https://developer.ercot.com/applications/marketrak/MarkeTrak_API_Dev_v1_2/)

### ERCOT Retail API

SOAP web service supporting Texas Standard Electronic Transactions (TX SET) between ERCOT, Transmission and Distribution Service Providers, and Retail Electric Providers — the machinery behind retail switching, enrollment, and move-in/move-out in the competitive Texas market. Contracts are published openly; the service itself is restricted to certified Market Participants.

- **Human URL:** [https://developer.ercot.com/api_specifications/retail/retail/](https://developer.ercot.com/api_specifications/retail/retail/)

#### Tags

- SOAP
- Retail
- Switching
- Market Participants

#### Properties

- [WSDL](https://raw.githubusercontent.com/ercot/api-specs/main/retail/RetailAPIConcreteWSDL-External.wsdl)
- [Schema](https://raw.githubusercontent.com/ercot/api-specs/main/retail/RetailAPIService.xsd)
- [Documentation](https://developer.ercot.com/api_specifications/retail/retail/)

## Common

- [Website](https://www.ercot.com/)
- [Developer Portal](https://developer.ercot.com/)
- [Documentation](https://developer.ercot.com/)
- [API Explorer](https://apiexplorer.ercot.com/)
- [Sign Up](https://apiexplorer.ercot.com/)
- [Plans](https://apiexplorer.ercot.com/products)
- [GitHub Organization](https://github.com/ercot)
- [Source Code](https://github.com/ercot/api-specs)
- [Open Data](https://data.ercot.com/)
- [Open Data](https://www.ercot.com/mp/data-products)
- [Issues](https://github.com/ercot/api-specs/issues)

## Energy Data Posture

| Dimension | Finding |
| --- | --- |
| Mandate regime | `none` — no consumer energy-data mandate applies to ERCOT itself |
| Mandate status | `not-applicable` — the Texas Green Button obligation sits with the TDUs via Smart Meter Texas, not with the ISO |
| Data standard | No consumer-data standard reference found; proprietary EMIL shape described by a real OpenAPI 3.0.1, plus SOAP/WS-* and TX SET for market participants |
| Consumer data API | No |
| Market data open | Yes — anonymous MIS report archives, anonymous dashboard JSON feeds, and a free self-serve OpenAPI-described REST API |
| Access gate | `self-serve` — email verification, then subscribe on the API Explorer Products page for an immediate key (US-only network access) |
| Auth model | `Ocp-Apim-Subscription-Key` (Azure APIM) **plus** an Azure AD B2C ID token from the `B2C_1_PUBAPI-ROPC-FLOW` policy, `grant_type=password` |

See [review.yml](review.yml) for the full evidence trail, every probed URL, and its HTTP status.
