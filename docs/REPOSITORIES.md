# Tyrelink repository and version-control policy

## Repositories

- `Tyrelink-frontend`: Astro storefront, product pages, assets and browser interactions.
- `Tyrelink-api`: Go API, PostgreSQL migrations and backend tests.
- `Tyrelink-infra`: VPS Nginx, systemd, backup and deployment configuration.
- `Tyrelink-docs`: product, brand, SEO, security, operations and release documentation.

The original `Tyrelink-web` monorepo is retained as a migration/reference repository until the split is verified. It must not be deleted without an explicit backup and migration sign-off.

## Branching

- `main` is always deployable.
- Work uses short-lived branches: `feat/*`, `fix/*`, `docs/*`, `security/*`.
- Every merge requires a review, build/test checks and a linked decision or issue.
- Tag releases using `vYYYY.MM.DD` or `vMAJOR.MINOR.PATCH` after frontend, API and infra versions are compatible.
- Never commit `.env`, passwords, tokens, private keys, customer exports or database dumps.

## Release order

1. Merge and tag API/migrations.
2. Apply migrations and deploy API to a canary VPS process.
3. Verify `/health`, database connectivity and smoke endpoints.
4. Build and deploy frontend.
5. Verify checkout/WhatsApp, catalog, contact and admin smoke journeys.
6. Record the release and rollback commit in the change log.
