factory_learnings:
  - id: PD-001
    relation: new
    related_makecepeit_rule: null
    type: global_rule
    agent: builder
    title: "Waive safety controls only explicitly"
    instruction: "If the owner drops a safety control (bot challenge, rate limit), add an explicit named opt-out setting; configured keys always win; the ready endpoint reports the degraded mode."
    rationale: "Owner declined Cloudflare and confirmed after the risk was raised; a forgotten key must not silently remove a control."
    confidence: high
    destination: ["CLAUDE.md", "rules/engineering.md"]
    project_specific: false
  - id: PD-002
    relation: refines
    related_makecepeit_rule: "MK-016"
    type: agent_rule
    agent: content
    title: "Answer legitimacy-adjacent queries honestly"
    instruction: "Exclude a query only if ranking needs pretending; if it has real legitimate users, target it with a page that states plainly what the product is not."
    rationale: "Owner chose honest 'not proof of income' pages over exclusion, accepting the conversion cost."
    confidence: medium
    destination: ["rules/seo-content.md", ".claude/agents/content.md"]
    project_specific: false
  - id: PD-003
    relation: new
    related_makecepeit_rule: null
    type: skill
    agent: builder
    title: "Review gate for regulated content"
    instruction: "Content stating tax, legal or financial facts ships noindex and outside sitemap, llms.txt and nav until a review record (name, role, date, version) exists; one registry feeds every surface so one approval publishes everywhere in one deploy."
    rationale: "Guides and calculators waited for owner approval and then published cleanly in one deploy."
    confidence: high
    destination: [".claude/skills/builder/SKILL.md", "rules/seo-content.md"]
    project_specific: false
  - id: PD-004
    relation: new
    related_makecepeit_rule: null
    type: skill
    agent: builder
    title: "Versioned rule engines"
    instruction: "Rule-based calculations cite official sources, are versioned per period, pinned by dependency-free golden tests, and sit behind a flag that refuses until that version has been reviewed."
    rationale: "About 40 tax rule sets shipped with a recorded approval per version and a check:tax suite."
    confidence: high
    destination: [".claude/skills/builder/SKILL.md"]
    project_specific: false
  - id: PD-005
    relation: refines
    related_makecepeit_rule: "MK-005"
    type: anti_pattern
    agent: builder
    title: "Global startup crash on config errors"
    instruction: "Never throw on config at startup or in next.config; validate per feature, fail that feature closed, log the detail, return 503 with a reason from /api/ready; treat blank env strings as unset."
    rationale: "One bad setting returned 500 on every SSR route; blank .env.example rows copied into Vercel broke the build."
    confidence: high
    destination: ["rules/engineering.md"]
    project_specific: false
  - id: PD-006
    relation: new
    related_makecepeit_rule: null
    type: acceptance_criterion
    agent: builder
    title: "No personal data in URLs"
    instruction: "No names, emails or ids of people in query strings (POST + httpOnly cookie for searches, no prefilled email in links); analytics strip queries and skip private routes."
    rationale: "A GET search put employee names into access logs, browser history and Referer headers."
    confidence: high
    destination: ["rules/engineering.md"]
    project_specific: false
  - id: PD-007
    relation: refines
    related_makecepeit_rule: "MK-026"
    type: skill
    agent: builder
    title: "Thin webhook, immutable paid artifacts"
    instruction: "Webhook verifies, dedupes and grants access only; heavy fulfilment runs idempotently on first access; paid artifacts are frozen snapshots with checksums; only a full refund or dispute revokes access."
    rationale: "Keeps the webhook fast and stops a render failure from losing a payment."
    confidence: medium
    destination: [".claude/skills/builder/SKILL.md"]
    project_specific: false
  - id: PD-008
    relation: refines
    related_makecepeit_rule: "MK-003"
    type: global_rule
    agent: builder
    title: "One source for public capability claims"
    instruction: "Feature status, supported regions and prices come from one module; page copy, FAQ structured data and llms.txt are generated from it, not written by hand per page."
    rationale: "Help, Trust and Pricing contradicted each other and the live product, including in structured data."
    confidence: high
    destination: ["CLAUDE.md", "rules/product.md"]
    project_specific: false
  - id: PD-009
    relation: refines
    related_makecepeit_rule: "MK-011"
    type: anti_pattern
    agent: design
    title: "Styling selectors that never render"
    instruction: "Before restyling, grep that the class is actually rendered; review automated style or token migrations for corrupted values and lost semantic colours."
    rationale: "Visual work went into unused globals.css classes; a token sweep broke 8-digit hex colours and greyed out error tints."
    confidence: high
    destination: ["rules/design.md"]
    project_specific: false
  - id: PD-010
    relation: new
    related_makecepeit_rule: null
    type: skill
    agent: builder
    title: "Blind deploy failure handling"
    instruction: "If a Vercel build fails and the log isn't readable: revert, record the hypothesis in DECISIONS, keep the working commit, and don't retry blindly; generate lockfiles with Vercel's npm major using --package-lock-only."
    rationale: "Sentry failed twice; an npm 10 lockfile was rejected by Vercel's npm ci."
    confidence: medium
    destination: ["rules/engineering.md"]
    project_specific: false
  - id: PD-011
    relation: refines
    related_makecepeit_rule: "MK-012"
    type: agent_rule
    agent: seo
    title: "No per-variant pages without demand"
    instruction: "Don't create one page per template, style or variant unless measured demand exists and each page can be distinct."
    rationale: "Template detail pages were skipped: no search demand, thin near-duplicates."
    confidence: medium
    destination: [".claude/agents/seo.md"]
    project_specific: false
  - id: PD-012
    relation: refines
    related_makecepeit_rule: "MK-018"
    type: skill
    agent: qa-launch
    title: "Zero-dependency site checker"
    instruction: "Keep a node script that crawls the live sitemap and checks status codes, broken links, canonicals, noindex vs sitemap, title and description lengths, JSON-LD, robots and llms files; run it after each deploy."
    rationale: "It replaced deleted CI with a read-only check and caught length issues on 23 pages."
    confidence: high
    destination: [".claude/skills/qa-launch/SKILL.md"]
    project_specific: false
  - id: PD-013
    relation: refines
    related_makecepeit_rule: "MK-001"
    type: global_rule
    agent: null
    title: "No CI means mandatory zero-install checks"
    instruction: "No installs or servers, but before every push run tsc, lint and dependency-free check scripts for business rules; after moving files, grep for runtime paths (process.cwd)."
    rationale: "Owner removed CI and tests; a moved font path would have broken every PDF and only tsc and checks stand in the way now."
    confidence: high
    destination: ["CLAUDE.md"]
    project_specific: false
  - id: PD-014
    relation: contradicts
    related_makecepeit_rule: "MK-002"
    type: global_rule
    agent: orchestrator
    title: "Regulated work is Done when gated"
    instruction: "Code tasks are Done without the owner; prices, regulatory rules and legal text are Done when built and waiting behind a gate, and go live only after a recorded owner approval."
    rationale: "Every PayDocs price, tax rule set and policy waited on a recorded owner approval."
    confidence: high
    destination: ["rules/launch.md", ".claude/agents/orchestrator.md"]
    project_specific: false
  - id: PD-015
    relation: new
    related_makecepeit_rule: null
    type: global_rule
    agent: builder
    title: "Baseline vendors are defaults, not requirements"
    instruction: "Cloudflare, Sentry and Resend are optional per project; when one is absent, record the fallback in DECISIONS (minimum: health and ready endpoints, platform deploy alerts, payment provider failure emails)."
    rationale: "Owner declined Cloudflare; Sentry failed to build; email waited on DNS."
    confidence: medium
    destination: ["rules/engineering.md"]
    project_specific: false