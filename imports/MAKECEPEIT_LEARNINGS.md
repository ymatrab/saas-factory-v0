factory_learnings:
  - id: MK-001
    type: global_rule
    agent: null
    title: "No local installs or local runs"
    instruction: "Never install deps or start a local server; verify via preview/production deploy."
    rationale: "Owner's standing rule; local disk is limited and the server is the test env."
    confidence: high
    destination: ["CLAUDE.md"]
    project_specific: false
  - id: MK-002
    type: global_rule
    agent: null
    title: "Done = verified live"
    instruction: "Mark work Done only after checking the production URL; note in the task what was and wasn't verifiable, then mark Done without waiting on the owner."
    rationale: "Green builds shipped a false competitor claim and hid unshipped subsystems."
    confidence: high
    destination: ["CLAUDE.md", "rules/launch.md", ".claude/agents/orchestrator.md"]
    project_specific: false
  - id: MK-003
    type: global_rule
    agent: null
    title: "Every public claim must be true"
    instruction: "Free/no-signup/limits/counts/competitor figures must match real behaviour or a live source; derive counts from data."
    rationale: "False 'no sign-up' and 'Free' on Pro pages were top audit findings."
    confidence: high
    destination: ["rules/product.md", "rules/seo-content.md"]
    project_specific: false
  - id: MK-004
    type: global_rule
    agent: null
    title: "No fake proof or personas"
    instruction: "No invented authors, counters or testimonials; use a team byline and real countable numbers."
    rationale: "Persona byline and download counter were removed."
    confidence: high
    destination: ["rules/product.md"]
    project_specific: false
  - id: MK-005
    type: global_rule
    agent: builder
    title: "Errors expose their cause"
    instruction: "Log and show admins the provider's raw error; users get a human message, never '{}' or a generic 502."
    rationale: "Retired AI model hid behind a generic 502 for five weeks."
    confidence: high
    destination: ["rules/engineering.md"]
    project_specific: false
  - id: MK-006
    type: skill
    agent: builder
    title: "Schema change that survives"
    instruction: "Migration ends with schema reload; code degrades if table absent; gates fail closed; owner applies one file at a time; probe each table via REST (206) before merging; keep /admin/health."
    rationale: "Unapplied migration silently gave free users unlimited paid features."
    confidence: high
    destination: ["rules/engineering.md", ".claude/skills/builder/SKILL.md"]
    project_specific: false
  - id: MK-007
    type: global_rule
    agent: builder
    title: "Stored config beats env"
    instruction: "When behaviour is wrong, check DB-stored settings (links, provider order) before code or env."
    rationale: "Env fallbacks were silently overridden by DB rows."
    confidence: high
    destination: ["rules/engineering.md"]
    project_specific: false
  - id: MK-008
    type: skill
    agent: builder
    title: "Resilient AI generation"
    instruction: "Ordered providers in DB config, per-attempt timeout, failover, quota cooldown, retired-model remap, inject current date, cap reasoning tokens, admin Test button sending the production payload, events with a reason field."
    rationale: "Single slow/dead provider took the generator down; metrics conflated auth gates with outages."
    confidence: high
    destination: ["rules/engineering.md", ".claude/skills/builder/SKILL.md"]
    project_specific: false
  - id: MK-009
    type: agent_rule
    agent: design
    title: "Pricing shows everything"
    instruction: "All plans side by side, full feature list in each card, comparison table; mark Pro items before the click."
    rationale: "Owner rejected a reduced pricing layout: users must compare."
    confidence: high
    destination: ["rules/design.md", ".claude/agents/design.md"]
    project_specific: false
  - id: MK-010
    type: acceptance_criterion
    agent: design
    title: "Accessibility minimums"
    instruction: "Tap targets >=44px, contrast >=4.5:1, announced errors, visible focus, no iOS input zoom."
    rationale: "Repeated a11y fix commits."
    confidence: high
    destination: ["rules/design.md"]
    project_specific: false
  - id: MK-011
    type: anti_pattern
    agent: design
    title: "Wholesale redesign"
    instruction: "Do not replace the established palette/fonts/geometry in one pass; change incrementally with evidence."
    rationale: "A full redesign was reverted to the original."
    confidence: medium
    destination: ["rules/design.md"]
    project_specific: false
  - id: MK-012
    type: skill
    agent: seo
    title: "Search-intent gate"
    instruction: "Classify keywords as retrieval/definition/creation; target creation; for low-CTR page-1 pages compare the query list to the title before judging."
    rationale: "Retrieval/definition pages ranked top-10 with ~0 clicks; one 'zero-click' page was really an intent mismatch."
    confidence: high
    destination: ["rules/seo-content.md", ".claude/skills/seo/SKILL.md"]
    project_specific: false
  - id: MK-013
    type: agent_rule
    agent: seo
    title: "Fix pages, don't delete"
    instruction: "Rewrite underperforming own pages in daily batches; 301 only competitor pages and true duplicates; state impressions and position before proposing removal."
    rationale: "73 retired pages had to be restored the same day."
    confidence: high
    destination: ["rules/seo-content.md", ".claude/agents/seo.md"]
    project_specific: false
  - id: MK-014
    type: agent_rule
    agent: seo
    title: "Bump sitemap dates per page"
    instruction: "Any visible content change moves that page to a fresh lastModified constant; never restamp untouched pages."
    rationale: "IndexNow silently skipped rewritten pages; false dates read as spam."
    confidence: high
    destination: ["rules/seo-content.md"]
    project_specific: false
  - id: MK-015
    type: agent_rule
    agent: seo
    title: "Stop technical polish once the crawl is clean"
    instruction: "When titles/meta/H1/canonical/schema show zero defects, shift effort to intent and authority, not more on-page tweaks."
    rationale: "Three audits plateaued at 80-83/100."
    confidence: high
    destination: [".claude/agents/seo.md"]
    project_specific: false
  - id: MK-016
    type: agent_rule
    agent: content
    title: "Cite, source, and stay legitimate"
    instruction: "Cite authorities for regulatory claims with a not-advice note; source competitor figures from their live page; exclude keywords that contradict product legitimacy."
    rationale: "Wrong competitor claim reached production; the fake-receipt cluster was excluded."
    confidence: high
    destination: ["rules/seo-content.md", ".claude/agents/content.md"]
    project_specific: false
  - id: MK-017
    type: skill
    agent: content
    title: "Scheduled publishing batch"
    instruction: "Validate keyword, dry-run publish script, set future publishedAt (spread out), idempotent ids, update ledger, confirm sitemap/IndexNow pickup; don't edit the newest ~20 posts."
    rationale: "Bulk drops perform worse; this cadence shipped 132 posts cleanly."
    confidence: high
    destination: [".claude/skills/content/SKILL.md"]
    project_specific: false
  - id: MK-018
    type: skill
    agent: qa-launch
    title: "Verify a production release"
    instruction: "Tree diff of shipping dirs; deploy status via GitHub statuses; curl changed routes; grep live HTML for new copy and banned claims; check sitemap lastmod; probe tables; write a verification note."
    rationale: "Commit logs and cherry-picks misreported what shipped."
    confidence: high
    destination: ["rules/launch.md", ".claude/skills/qa-launch/SKILL.md"]
    project_specific: false
  - id: MK-019
    type: global_rule
    agent: qa-launch
    title: "Remove dropped services completely"
    instruction: "Same day a service is dropped, delete its DNS records and git/CI integrations."
    rationale: "Dangling CNAME caused a subdomain takeover; a stale check was always red."
    confidence: high
    destination: ["rules/launch.md"]
    project_specific: false
  - id: MK-020
    type: global_rule
    agent: orchestrator
    title: "Task system discipline"
    instruction: "Fetch the brief first, set In progress as a lock, sync only at start/end, write outcome-phrased standalone task bodies, check plans against code before seeding."
    rationale: "Per-step syncing burned the quota; pointer-to-markdown tasks dangled."
    confidence: high
    destination: [".claude/agents/orchestrator.md"]
    project_specific: false
  - id: MK-021
    type: agent_rule
    agent: orchestrator
    title: "Phase order is a dependency chain"
    instruction: "Stop revenue leaks, then automate fulfilment, then build trust, then grow; never pull growth work forward."
    rationale: "Growth into a leaky funnel loses buyers invisibly."
    confidence: high
    destination: [".claude/agents/orchestrator.md", "rules/product.md"]
    project_specific: false
  - id: MK-022
    type: global_rule
    agent: null
    title: "Metered APIs and batches"
    instruction: "Set limits, save dated responses, reuse snapshots, no crons without asking; keep a local id ledger during external batch writes; report a paid-API 403 once and ask."
    rationale: "Balances and quotas ran dry mid-job; repeated 403 investigations wasted audits."
    confidence: high
    destination: ["rules/engineering.md"]
    project_specific: false
  - id: MK-023
    type: global_rule
    agent: null
    title: "Re-verify inherited diagnoses; latest owner word wins"
    instruction: "Check memory/audit/plan conclusions against current data before acting; when the owner reverses a decision, update memory immediately."
    rationale: "Three wrong diagnoses and a stale 'paused' memory caused wrong work and answers."
    confidence: high
    destination: ["CLAUDE.md"]
    project_specific: false
  - id: MK-024
    type: global_rule
    agent: null
    title: "Defaults over questions"
    instruction: "Pick sensible defaults and proceed; ask only for production merges, spend, or genuinely owner-only decisions."
    rationale: "Owner is busy and wants minimal back-and-forth."
    confidence: high
    destination: ["CLAUDE.md"]
    project_specific: false
  - id: MK-025
    type: agent_rule
    agent: builder
    title: "Build-time guard for critical copy"
    instruction: "Fail the build when a business invariant is violated in copy (e.g. a paid page says 'free')."
    rationale: "A generation script kept reintroducing false 'free' claims."
    confidence: medium
    destination: [".claude/agents/builder.md"]
    project_specific: false
  - id: MK-026
    type: agent_rule
    agent: builder
    title: "Cancelled is not revoked"
    instruction: "For one-time passes, a cancelled plan stays entitled until period end."
    rationale: "Paying customers were cut off mid-period."
    confidence: medium
    destination: [".claude/agents/builder.md"]
    project_specific: false