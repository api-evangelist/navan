# Navan (navan)

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
