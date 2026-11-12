# Tyrelink security baseline

- Never commit `.env` or admin tokens.
- Admin API uses an expiring signed admin session token from `/v1/admin/login`; production should store admin credentials in a secret manager and add a database-backed user/role system.
- Public prices are indicative and must be confirmed before order acceptance.
- Do not put customer phone numbers or WhatsApp message content in analytics.
- Rate-limit order-lead endpoints before production exposure and add bot protection.
- The API has a conservative in-memory per-client rate limit for the current single-instance baseline; use an edge/shared limiter for multi-instance production.
- Use HTTPS, HSTS, CSP, `X-Content-Type-Options`, `X-Frame-Options`, strict referrer policy and least-privilege database credentials in production.
- Keep PostgreSQL private; expose only the frontend and API through the hosting edge.
- Review `npm audit`, Go dependency updates and secret scanning in CI.
