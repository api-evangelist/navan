# Navan (navan)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Navan (formerly **TripActions**, rebranded to Navan in February 2022) is a corporate travel, expense, and corporate card management platform. Its public developer surface centers on the **Navan Expense API** - an OAuth 2.0 client-credentials REST API for retrieving and updating transactions, fees, adjustments, receipts, and custom fields - plus a **Travel / User Management API** for provisioning users and reading booking data, and **webhooks** for change notifications. Navan also publishes an **MCP server** for connecting AI assistants to Navan data. The API base is `https://api.navan.com`; access is scoped (e.g. `bookings:read`, `users:read`, `users:write`, `users:delete`, expense read/write).

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/navan/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/navan/refs/heads/main/apis.yml)

## Tags

- Corporate Travel
- Expense Management
- Corporate Cards
- Spend Management
- T&E
- Fintech
- Business Travel

## Timestamps

- **Created:** 2026-07-03
- **Modified:** 2026-07-03

## Authentication

OAuth 2.0 **client-credentials** flow. An admin generates a `client_id` / `client_secret` in the Navan app under **Settings > Integrations (API)**, then exchanges them for a short-lived Bearer access token at the token URL and calls the API with `Authorization: Bearer <token>`.

- **US token URL:** `https://app.navan.com/ta-auth/oauth/token`
- **EU token URL:** `https://app-fra.navan.com/ta-auth/oauth/token`

The `ta-auth` path is a survival of the legacy **TripActions** naming. Different integration guides also reference `https://api.navan.com/ta-auth/oauth/token` and `https://api.navan.com/auth/v1/token` variants - confirm the current token URL in the Navan developer portal.

## APIs

### Navan Expense Transactions API

Retrieve and update expense transactions across Navan card, Connect (external card), manual/payroll, and repayment types, with a generic multi-type list, single-transaction lookup, and batch update. **Endpoints confirmed** against the Navan Expense API reference.

- **Base URL:** `https://api.navan.com/v1/expense`
- **Human URL:** [https://developer.navan.com/api/](https://developer.navan.com/api/)

### Navan Expense Fees and Adjustments API

Read direct-reimbursement, FX, and platform fees, credit/debit memo adjustments, daily rebates, and dispute transactions. **Endpoints confirmed.**

- **Base URL:** `https://api.navan.com/v1/expense`

### Navan Expense Receipts API

Retrieve receipt image URLs for a transaction, follow a download redirect, and batch-fetch receipt URLs by date. **Endpoints confirmed.**

- **Base URL:** `https://api.navan.com/v1/expense`

### Navan Expense Custom Fields API

List and read company custom fields (Navan's mechanism for cost-center / department / GL coding), batch-manage a field's options, and poll asynchronous jobs. **Endpoints confirmed.**

- **Base URL:** `https://api.navan.com/v1/expense`

### Navan Users API

List, retrieve, create, update, and deactivate users under `travel/v1` with cursor pagination and `users:read` / `users:write` / `users:delete` scopes (deactivation is a soft delete). **Endpoints confirmed** against third-party user-management integration documentation.

- **Base URL:** `https://api.navan.com/travel/v1`

### Navan Bookings API

Read booking (trip) records to transfer travel data into downstream ERP, data-warehouse, and reporting systems, mirroring Navan's booking report columns. The `bookings:read` scope is confirmed; the **exact endpoint paths are modeled** because the full reference is gated.

- **Base URL:** `https://api.navan.com/travel/v1`

### Navan Webhooks API

Register and manage webhook subscriptions so Navan can POST change notifications to your endpoint. Webhooks are advertised as a first-class Expense API feature; the **subscription-management paths are modeled** because the detailed webhook reference is gated. There is **no public WebSocket API** - server-push is delivered via webhooks.

- **Base URL:** `https://api.navan.com/v1/expense`

## Endpoint Confidence

- **Confirmed** (grounded in Navan's Expense API reference and third-party integration guides): all `v1/expense/*` transaction, fee, adjustment, receipt, and custom-field endpoints, and the `travel/v1/users` endpoints.
- **Modeled** (capability/scope documented by Navan, exact path inferred behind a gated reference, flagged `x-endpoint-status: modeled` in the OpenAPI): the `travel/v1/bookings` endpoints and the `v1/expense/webhooks` subscription-management endpoints.

Navan platform concepts such as departments, cost centers, and travel/spend policies are surfaced primarily through **custom fields** and admin configuration rather than as separate documented public API resources, so they are not modeled as standalone APIs here.

## Pricing

Navan does not publish fixed list pricing. Three commercial motions are commonly referenced: **Business Travel** at no platform fee (funded by supplier commissions and per-trip booking fees), **Business Expense** as a per-user subscription (widely reported around **$15/user/month**, with a small number of users free), and a custom **Enterprise** agreement for unified travel + expense. API access is included with the subscription and is not sold as a separate metered product. See [plans/navan-plans-pricing.yml](plans/navan-plans-pricing.yml).

## Rate Limits

Navan does not publish numeric rate-limit tiers. Handle HTTP 429, use exponential backoff with jitter, honor `Retry-After`, and use cursor pagination with date filters for bulk extraction. See [rate-limits/navan-rate-limits.yml](rate-limits/navan-rate-limits.yml).

## Common Properties

- [GitHub Organization](https://github.com/navan-public)
- [LinkedIn](https://www.linkedin.com/company/navan)
- [Website](https://navan.com)
- [Documentation](https://developer.navan.com/)
- [Plans](plans/navan-plans-pricing.yml)
- [Rate Limits](rate-limits/navan-rate-limits.yml)
- [Fin Ops](finops/navan-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
