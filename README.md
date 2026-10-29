# ERCOT

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

The Electric Reliability Council of Texas (ERCOT) is the independent system operator that manages the flow of electric power to roughly 27 million Texas customers on the ERCOT Interconnection, running the wholesale Day-Ahead and Real-Time energy markets, ancillary services, congestion revenue rights, and retail switching for the competitive Texas market. Its home market is the United States (Texas). ERCOT sits at the wholesale/system-operator layer of the energy value chain, upstream of the transmission and distribution utilities (Oncor, CenterPoint, AEP Texas, TNMP) and the retail electric providers that serve end customers. Its API posture is a clean split: market and grid data are genuinely open — ERCOT publishes a real, versioned OpenAPI 3.0 for the Public Data API covering 106 EMIL data-product endpoints (locational marginal prices, settlement point prices, system load, wind and solar production, ancillary services, outage capacity), and the Market Information System still serves public report archives anonymously with no account at all. Consumer energy data is a different story: ERCOT operates no consumer usage API and implements no Green Button / ESPI surface. Texas residential interval data lives in Smart Meter Texas, which is operated by the joint Transmission and Distribution Utilities under PUCT oversight, not by ERCOT. The market-participant SOAP estate (ERCOT Web Services, MarkeTrak, Retail API) is documented publicly on GitHub but reachable only by certified market participants.

**Areas:** Energy · United States · Electricity · Energy Markets · Grid · System Operator · Texas · Renewables · Demand Response · Open Data · ERCOT

## ERCOT on APIs.io

Everything profiled for ERCOT is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/ercot/](https://apis.io/providers/ercot/)** — or go straight to one of the APIs or properties below.

### APIs (41)

- [ERCOT ESR Public Data API](https://apis.io/apis/ercot/ercot-esr-public-data-api/) — Energy Storage Resource public data, launched May 29, 2025 per the ERCOT Public Data API release notes, beginning with four-second ESR charging MW telemetry…
- [ERCOT Web Services (EWS)](https://apis.io/apis/ercot/ercot-web-services/) — ERCOT's SOAP web-services estate for Nodal market participants — the Market Information Service, Market Transaction Service (bid and offer submission via…
- [ERCOT MarkeTrak API](https://apis.io/apis/ercot/ercot-marketrak-api/) — SOAP API over MarkeTrak, ERCOT's retail-market issue tracking system, supporting QueryList, QueryDetail, Update, and Submit operations against retail…
- [ERCOT Retail API](https://apis.io/apis/ercot/ercot-retail-api/) — SOAP web service supporting Texas Standard Electronic Transactions (TX SET) between ERCOT, Transmission and Distribution Service Providers, and Retail…
- [ERCOT EMIL Products API](https://apis.io/apis/ercot/ercot-emil-products-api/) — The EMIL Products API from ERCOT — 3 operation(s) for emil products.
- [ERCOT NP3 233 CD API](https://apis.io/apis/ercot/ercot-np3-233-cd-api/) — <b>Hourly Resource Outage Capacity</b><br/><br/>This report includes all approved and accepted Planned, Forced and Maintenance Resource outages EXCEPT…
- [ERCOT NP3 565 CD API](https://apis.io/apis/ercot/ercot-np3-565-cd-api/) — <b>Seven-Day Load Forecast by Model and Weather Zone</b><br/><br/>Hourly system-wide Mid-Term Load Forecasts (MTLFs) for all forecast models with an…
- [ERCOT NP3 566 CD API](https://apis.io/apis/ercot/ercot-np3-566-cd-api/) — <b>Seven-Day Load Forecast by Model and Study Area</b><br/><br/>Forecasted hourly demands by Study Area, for the current day plus the next seven days.
- [ERCOT NP3 910 ER API](https://apis.io/apis/ercot/ercot-np3-910-er-api/) — <b>2-Day Real Time Gen and Load Data Reports</b><br/><br/>This report will contain all 48 Hour disclosure data related to Real Time. The following…
- [ERCOT NP3 911 ER API](https://apis.io/apis/ercot/ercot-np3-911-er-api/) — <b>2-Day Ancillary Services Reports</b><br/><br/>This report will contain all 48 Hour disclosure data related to DAM. The following individual files are…
- [ERCOT NP3 965 ER API](https://apis.io/apis/ercot/ercot-np3-965-er-api/) — <b>60-Day SCED Disclosure Reports</b><br/><br/>This report will contain all 60 day disclosure data related to SCED. The following individual files are…
- [ERCOT NP3 966 ER API](https://apis.io/apis/ercot/ercot-np3-966-er-api/) — <b>60-Day DAM Disclosure Reports</b><br/><br/>This report will contain all 60 day disclosure data related to DAM. The following individual files are…
- [ERCOT NP3 990 EX API](https://apis.io/apis/ercot/ercot-np3-990-ex-api/) — <b>60-Day SASM Disclosure Reports</b><br/><br/>This report will contain all 60 day disclosure data related to SASM for Generation and Load Resources. The…
- [ERCOT NP3 991 EX API](https://apis.io/apis/ercot/ercot-np3-991-ex-api/) — <b>60-Day COP All Updates</b><br/><br/>This report will contain all iterative Current Operating Plan (COP) submissions where a change has occurred for the…
- [ERCOT NP4 159 CD API](https://apis.io/apis/ercot/ercot-np4-159-cd-api/) — <b>Load Distribution Factors</b><br/><br/>Load forecast distribution factors from which Market Participants can calculate Load at the Electrical Bus level…
- [ERCOT NP4 179 CD API](https://apis.io/apis/ercot/ercot-np4-179-cd-api/) — <b>Total Ancillary Service Offers</b><br/><br/>The total quantity in MW of Offers per Ancillary Service per hour from the Day-Ahead Market for the last…
- [ERCOT NP4 183 CD API](https://apis.io/apis/ercot/ercot-np4-183-cd-api/) — <b>DAM Hourly LMPs</b><br/><br/>The Hourly Locational Marginal Prices per electrical bus from the Day-Ahead Market for the last thirty days on a daily basis.
- [ERCOT NP4 188 CD API](https://apis.io/apis/ercot/ercot-np4-188-cd-api/) — <b>DAM Clearing Prices for Capacity</b><br/><br/>The Market Clearing Prices for Capacity for all Ancillary Services from the Day-Ahead Market for the last…
- [ERCOT NP4 190 CD API](https://apis.io/apis/ercot/ercot-np4-190-cd-api/) — <b>DAM Settlement Point Prices</b><br/><br/>The Settlement Point Prices for all Resource Nodes, Load Zones, and Trading Hubs from the Day-Ahead Market for…
- [ERCOT NP4 191 CD API](https://apis.io/apis/ercot/ercot-np4-191-cd-api/) — <b>DAM Shadow Prices</b><br/><br/>The active and binding constraints as well as the associated shadow prices from the Day-Ahead Market for the last thirty…
- [ERCOT NP4 196 M API](https://apis.io/apis/ercot/ercot-np4-196-m-api/) — <b>DAM Price Corrections</b><br/><br/>Day-Ahead Market price corrections.
- [ERCOT NP4 197 M API](https://apis.io/apis/ercot/ercot-np4-197-m-api/) — <b>RTM Price Corrections</b><br/><br/>Real-Time Market price corrections.
- [ERCOT NP4 33 CD API](https://apis.io/apis/ercot/ercot-np4-33-cd-api/) — <b>DAM Ancillary Service Plan</b><br/><br/>Ancillary Service requirements by type and quantity for each hour of the current day plus the next 6 days.
- [ERCOT NP4 523 CD API](https://apis.io/apis/ercot/ercot-np4-523-cd-api/) — <b>DAM System Lambda</b><br/><br/>System lambda of each successful DAM.
- [ERCOT NP4 732 CD API](https://apis.io/apis/ercot/ercot-np4-732-cd-api/) — <b>Wind Power Production - Hourly Averaged Actual and Forecasted Values</b><br/><br/>This report is posted every hour and includes System-wide and Regional…
- [ERCOT NP4 733 CD API](https://apis.io/apis/ercot/ercot-np4-733-cd-api/) — <b>Wind Power Production - Actual 5-Minute Averaged Values</b><br/><br/>This report is posted every 5 minutes and includes System-wide and Regional actual…
- [ERCOT NP4 737 CD API](https://apis.io/apis/ercot/ercot-np4-737-cd-api/) — <b>Solar Power Production - Hourly Averaged Actual and Forecasted Values</b><br/><br/>This report includes System-wide actual hourly averaged solar power…
- [ERCOT NP4 738 CD API](https://apis.io/apis/ercot/ercot-np4-738-cd-api/) — <b>Solar Power Production - Actual 5-Minute Averaged Values</b><br/><br/>This report is posted every 5 minutes and includes System-wide actual 5-minute…
- [ERCOT NP4 742 CD API](https://apis.io/apis/ercot/ercot-np4-742-cd-api/) — <b>Wind Power Production - Hourly Averaged Actual and Forecasted Values by Geographical Region</b><br/><br/>This report is posted every hour and includes…
- [ERCOT NP4 743 CD API](https://apis.io/apis/ercot/ercot-np4-743-cd-api/) — <b>Wind Power Production - Actual 5-Minute Averaged Values by Geographical Region</b><br/><br/>This report is posted every 5 minutes and includes…
- [ERCOT NP4 745 CD API](https://apis.io/apis/ercot/ercot-np4-745-cd-api/) — <b>Solar Power Production - Hourly Averaged Actual and Forecasted Values by Geographical Region</b><br/><br/>This report is posted every hour and includes…
- [ERCOT NP4 746 CD API](https://apis.io/apis/ercot/ercot-np4-746-cd-api/) — <b>Solar Power Production - Actual 5-Minute Averaged Values by Geographical Region</b><br/><br/>This report is posted every 5 minutes and includes…
- [ERCOT NP6 322 CD API](https://apis.io/apis/ercot/ercot-np6-322-cd-api/) — <b>SCED System Lambda</b><br/><br/>System lambda of each successful SCED.
- [ERCOT NP6 345 CD API](https://apis.io/apis/ercot/ercot-np6-345-cd-api/) — <b>Actual System Load by Weather Zone</b><br/><br/>Report of Actual hourly load data by weather zone and ERCOT total.
- [ERCOT NP6 346 CD API](https://apis.io/apis/ercot/ercot-np6-346-cd-api/) — <b>Actual System Load by Forecast Zone</b><br/><br/>A daily report of Actual System Load by Forecast Zone for each hour of the previous operating day.
- [ERCOT NP6 787 CD API](https://apis.io/apis/ercot/ercot-np6-787-cd-api/) — <b>LMPs by Electrical Bus</b><br/><br/>The Locational Marginal Price for each Electrical Bus, normally produced by SCED every five minutes.
- [ERCOT NP6 788 CD API](https://apis.io/apis/ercot/ercot-np6-788-cd-api/) — <b>LMPs by Resource Nodes, Load Zones and Trading Hubs</b><br/><br/>The Locational Marginal Price for each Settlement Point, normally produced by SCED every…
- [ERCOT NP6 86 CD API](https://apis.io/apis/ercot/ercot-np6-86-cd-api/) — <b>SCED Shadow Prices and Binding Transmission Constraints</b><br/><br/>The report for Shadow Prices of binding/violated constraints in SCED. The report…
- [ERCOT NP6 905 CD API](https://apis.io/apis/ercot/ercot-np6-905-cd-api/) — <b>Settlement Point Prices at Resource Nodes, Hubs and Load Zones</b><br/><br/>Settlement Point Price for each Settlement Point, produced from SCED LMPs…
- [ERCOT NP6 970 CD API](https://apis.io/apis/ercot/ercot-np6-970-cd-api/) — <b>RTD Indicative LMPs by Resource Nodes, Load Zones and Hubs</b><br/><br/>This report is posted after every Look Ahead RTD run and includes indicative LMPs…
- [ERCOT Versioning API](https://apis.io/apis/ercot/ercot-versioning-api/) — The Versioning API from ERCOT — 1 operation(s) for versioning.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Ercot Ews Notifications](https://apis.io/asyncapis/ercot/ercot-ews-notifications/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [ercot-public-data](https://apis.io/servers/ercot/ercot-public-data/)

#### Collections (1)

Postman and Open Collection request collections.

- [ERCOT Public API Client/Developer Documentation](https://apis.io/collections/ercot/open-ercot-public-data-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Ercot Public Data Api Overlay](https://apis.io/overlays/ercot/ercot-public-data-api-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Ercot Authentication](https://apis.io/security/ercot/ercot-authentication/)
- [Ercot Domain Security](https://apis.io/security/ercot/ercot-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Ercot Scopes](https://apis.io/scopes/ercot/ercot-scopes/)

#### Rate limits (1)

Published request limits.

- [Ercot Rate Limits](https://apis.io/rate-limits/ercot/ercot-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.ercot.com/)
- [Documentation](https://developer.ercot.com/)
- [Getting started](https://developer.ercot.com/applications/pubapi/user-guide/registration-and-authentication/)
- [API reference](https://apiexplorer.ercot.com/api-details#api=pubapi-apim-api)
- [Sign up](https://apiexplorer.ercot.com/)
- [Support](https://developer.ercot.com/support/support/)
- [Blog](https://www.ercot.com/news)
- [Terms of service](https://www.ercot.com/help/terms/data-portal)
- [Privacy policy](https://www.ercot.com/help/privacy)
- [GitHub](https://github.com/ercot)

## API Evangelist rating

**Kin Score 50.2** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 60.7 |
| Contract quality | 54.3 |
| Contract governance | 4.5 |
| Operational transparency | 55.3 |
| Developer ergonomics | 58.9 |
| Access clarity | 34.2 |

**Agent readiness 41.7** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | na |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | na |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | derived (partial credit) |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | na |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 41.0** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/ercot/](https://apis.io/providers/ercot/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for ERCOT: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/ercot/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
