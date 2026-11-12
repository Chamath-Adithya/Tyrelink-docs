# Tyrelink release and VPS runbook

## Repositories

| Repository | Deployable output | Owner boundary |
|---|---|---|
| `Tyrelink-frontend` | Astro `dist/` | storefront, SEO, assets, browser UX |
| `Tyrelink-api` | Go API binary/container | API, migrations, auth, leads |
| `Tyrelink-infra` | reverse proxy, systemd, backups | VPS topology and operations |
| `Tyrelink-docs` | contracts and policies | release, content, security and ownership |

`Tyrelink-web` is retained as the historical integration copy until the split
repos have been deployed and smoke-tested. Do not delete it without an explicit
backup and sign-off.

## Release order

1. Review API migration and contract changes. Back up PostgreSQL.
2. Deploy the API binary, run forward-compatible migrations, and check `/health`.
3. Deploy the frontend `dist/` output and verify the same-origin `/api/` proxy.
4. Run mobile, Sinhala, keyboard, WhatsApp, warranty and order smoke tests.
5. Tag the tested commits and record the frontend/API/infra versions together.

## Rollback

Keep the previous frontend directory and API binary. Roll back the frontend
first for presentation regressions. Roll back the API only when migrations are
backward-compatible; destructive database changes require a restore plan and
must never be reversed by guessing.

## VPS topology

Internet → Nginx/Caddy TLS termination → static frontend and `/api/` proxy →
Go API → private PostgreSQL. PostgreSQL has no public port in production.
Secrets live in `/etc/tyrelink/` with restrictive permissions, not Git.

## Backups and operations

Use the infra backup script daily, retain at least 14 days, encrypt off-host
copies, and perform a restore drill before launch and quarterly thereafter.
Monitor API health, disk, memory, certificate expiry, backup freshness, 5xx
rate, lead errors and authentication failures. Keep logs redacted and rotate
them according to the privacy retention policy.

## Launch gates

- `npm ci && npm run build` passes in frontend.
- `go test ./... && go vet ./...` passes in API.
- No critical/high production dependency findings without a documented owner.
- No placeholder links or demo-only claims on public pages.
- HTTPS, CSP, HSTS, rate limiting, private DB and admin session controls are
  verified in staging.
- Prices, fitment, warranty, delivery, hours and Sinhala copy have an owner.
