# Tyrelink API contract (v1)

The storefront consumes the API through the reverse proxy path `/api/`.
Responses use JSON and include a request ID on errors. IDs are opaque and must
not expose sequential database identifiers.

## Public endpoints

- `GET /v1/products` — published catalogue, with stable SKU, category, size,
  typed specifications, price kind and freshness metadata.
- `GET /v1/products/{id}` — one published product.
- `POST /v1/order-leads` — schema-validated enquiry; requires contact consent,
  body-size limits and idempotency protection.
- `POST /v1/order-leads/{id}/whatsapp-link` — creates a user-initiated,
  prefilled WhatsApp handoff. It is not order confirmation.
- `GET /v1/warranty/{reference}` and `GET /v1/orders/{reference}` — only after
  privacy-safe authenticated or possession-based lookup is implemented; do not
  expose enumerable records.

## Admin boundary

Admin CRUD is authenticated server-side with HttpOnly/Secure/SameSite sessions,
CSRF/origin checks, RBAC, audit events and rate limiting. Product price and
availability are looked up server-side; clients cannot submit authoritative
price, stock or order state.

## Compatibility policy

Additive fields are backward-compatible. Renames, removals and migration
changes require a new API version or a staged deprecation. Frontend and API
release notes must record the compatible commit/tag pair.
