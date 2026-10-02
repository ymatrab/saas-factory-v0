# QA & Launch Rules

- A successful local page render is not sufficient for launch readiness.
- Run configured lint/typecheck/tests/build before declaring done (on the server build).
- Verify key production user flows.
- Verify auth/RLS when relevant.
- Verify environment variables and secret handling.
- Verify production deployment rather than assuming local behavior transfers.

## Learned rules
- **Done = verified live.** A green build is not done. Check the production/preview URL, note in the task what was and wasn't verifiable, then mark Done without waiting on the owner.
- **Regulated work is Done when gated.** Prices, tax/legal/financial rules and legal text are Done when built and held behind a gate (noindex, flag off). They go live only after a recorded owner approval (name, role, date, version). Ordinary code tasks never wait on the owner.
- **Verify what shipped, not what was committed.** Commit logs and cherry-picks misreport releases; check the live output (qa-launch skill).
- **Remove dropped services completely.** The same day a service is dropped, delete its DNS records and its git/CI integrations. Dangling CNAMEs enable subdomain takeover.
