# Builder Skill Set

Use this skill for implementation work on the default SaaS stack.

## Core checklist
1. Inspect relevant existing files first.
2. Choose the simplest architecture that satisfies the real product requirements.
3. Implement end-to-end behavior, not visual stubs.
4. For Supabase user data, design schema + indexes + ownership + RLS together.
5. Keep privileged service credentials server-only.
6. Add/update `.env.example` for every required variable (no blank rows that could be copied into the host as empty values).
7. Avoid dependencies when platform/native capabilities suffice.
8. Validate the changed path before moving on.

## Procedures (use when the task matches)

### Schema change that survives
1. Each migration ends with a schema-cache reload (`notify pgrst, 'reload schema';`).
2. Code degrades gracefully if the table/column is absent; paid gates fail closed.
3. Give the owner one migration file at a time to apply.
4. Before merging, probe each new table via the REST API (expect 200/206, not 404).
5. Keep an `/admin/health` view that lists required tables and settings.

### Resilient AI generation
1. Ordered provider list stored in DB config, not hardcoded.
2. Per-attempt timeout → fail over to the next provider; cool down providers that hit quota.
3. Remap retired model ids; inject the current date into prompts; cap reasoning/output tokens.
4. Admin "Test" button that sends the exact production payload.
5. Log one event per attempt with a `reason` field (timeout, quota, auth, gate), so that auth/plan gates aren't counted as outages.

### Payments and paid artifacts
1. The webhook only verifies the signature, dedupes the event id and grants access. Keep it fast.
2. Heavy fulfilment (render, email, export) runs idempotently on first access or in a retryable job, so a render failure never loses a payment.
3. Paid artifacts are frozen snapshots with a checksum, never re-rendered from live data.
4. Entitlement: cancellation runs to period end; full refund or dispute revokes.

### Regulated content gate (tax, legal, financial facts)
1. One registry lists each guide/calculator with its review record: reviewer name, role, date, content version.
2. With no record for the current version: noindex, excluded from sitemap, llms.txt and nav.
3. Every surface reads the registry, so one approval publishes everywhere in one deploy.

### Versioned rule engines (calculations based on official rules)
1. Each rule set cites its official source and is versioned per period (e.g. tax year).
2. Pin it with dependency-free golden tests (`node` script, no install needed).
3. Put it behind a flag that refuses to calculate until that version's review is recorded.

### Copy invariant checks
Where a business invariant in copy has regressed before (e.g. a paid page saying "free"), add a dependency-free check script and fail the build when it is violated.
