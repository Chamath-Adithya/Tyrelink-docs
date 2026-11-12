# Tyrelink application architecture

Tyrelink is an Astro storefront backed by a Go API and PostgreSQL. The first release is WhatsApp-first: public sample/indicative prices are displayed, but stock, fitment, final price and order acceptance are confirmed by staff.

## Monorepo

```text
Tyrelink-web/
├── src/                    # Astro storefront and future React islands
├── public/                 # optimized public media
├── backend/
│   ├── cmd/api/             # Go HTTP API
│   └── migrations/          # PostgreSQL schema
├── docker-compose.yml       # local PostgreSQL
├── docs/                    # product, architecture and launch docs
└── Makefile
```

## Lappix feature parity roadmap

- Storefront: home, shop, categories, product detail, search, filters and related products.
- Conversion: cart-like selection, quick WhatsApp order modal, lead capture before redirect and floating WhatsApp support.
- Trust: warranty checker, order tracking, policies, FAQ, contact and about pages.
- Admin: authenticated product/catalogue editor, campaigns, featured/trending controls and lead status management.
- Tyrelink-specific: vehicle/size fitment finder, tyre-age/manufacture-date fields, fitting locations, garage packages, delivery coverage and Sinhala content.

## Backend boundaries

The catalogue and lead APIs are intentionally separated from the frontend. An inventory adapter, payment adapter and partner-service adapter can be added later without replacing the storefront or database model.
