# Engineering Rules

- Prefer simple Next.js architecture for simple SaaS products.
- Use Supabase capabilities before inventing unnecessary infrastructure.
- Protect secrets and enforce server/client boundaries.
- Use RLS for user-owned Supabase data.
- Keep .env.example accurate and secret-free.
- Preserve stable existing behavior during improvements.

## Learned rules

### Failure handling
- **Errors expose their cause.** Log the provider's raw error and show it to admins; users get a human message, never `{}` or a bare 502.
- **Never crash globally on config.** Do not throw on config at startup or in `next.config`. Validate per feature, fail that feature closed, log the detail, and report it from `/api/ready` (503 + reason). Treat blank env strings as unset.
- **Paid gates fail closed.** If a table, setting or check is missing, deny the paid feature; never grant it by default.
- **Check stored config before code.** When behavior is wrong, check DB-stored settings (links, provider order, flags) before code or env. DB rows override env fallbacks.

### Safety and privacy
- **Waive safety controls only explicitly.** If the owner drops a control (bot challenge, rate limit), add a named opt-out setting. A configured key always re-enables the control, and the ready endpoint reports the degraded mode. Record it in PROJECT.md.
- **No personal data in URLs.** No names, emails or person ids in query strings: use POST + httpOnly cookie for searches and no prefilled emails in links. Analytics strip query strings and skip private routes.

### Billing
- **Cancelled is not revoked.** A cancelled plan or time-limited pass stays entitled until period end. Only a full refund or dispute revokes access immediately.

### Vendors, APIs and deploys
- **Baseline vendors are defaults, not requirements.** Cloudflare, Sentry and Resend are optional per project. When one is absent, record the fallback in PROJECT.md. Minimum: health + ready endpoints, platform deploy alerts, payment-provider failure emails.
- **Metered APIs and batches.** Set limits, save dated responses and reuse snapshots. No crons or scheduled jobs without asking. Keep a local id ledger during external batch writes. Report a paid-API 403 once and ask; do not keep re-investigating it.
- **Unreadable build failure.** If a deploy fails and the log can't be read: revert to the last working commit, record the hypothesis in PROJECT.md, and do not retry blindly. Lockfiles must match the host's package-manager major version.
- **Next.js client boundary.** A server component may import components from a `"use client"` module, never plain values (arrays, objects, helpers): it receives a reference, not the data, and the build fails at prerender (`x.map is not a function`). Keep shared data in a plain module. `tsc` does not catch this.
- **Read the build log before fixing.** When a deploy fails, get the log first (host dashboard via the owner's browser if the API scope is wrong); re-run typecheck after every edit, including one-line fixes.
- **Moved files.** After moving files, grep for runtime paths (`process.cwd()`, fs reads) that the type checker cannot catch.
