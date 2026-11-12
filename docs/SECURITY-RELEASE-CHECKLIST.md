# Security release checklist

- [ ] Dependencies scanned in frontend and API CI; critical/high findings have
  a fix, exception owner and expiry.
- [ ] Admin uses production session authentication, RBAC, CSRF/origin checks,
  MFA policy and audit logging; no bearer-prefix or localStorage auth.
- [ ] API request bodies have strict schemas, size limits, opaque IDs,
  idempotency and redacted errors/logs.
- [ ] Rate limiting is enforced at the trusted proxy/shared store and does not
  trust arbitrary client `X-Forwarded-For` values.
- [ ] PostgreSQL is private; secrets are outside Git; backups are encrypted and
  a restore test is recorded.
- [ ] HTTPS, HSTS, CSP, frame denial, nosniff, referrer and permissions headers
  are verified on the deployed host.
- [ ] Warranty/order lookup does not permit unauthenticated enumeration.
- [ ] Analytics excludes phone, message, address and vehicle identifiers.
- [ ] Release has rollback version, migration compatibility and incident owner.
