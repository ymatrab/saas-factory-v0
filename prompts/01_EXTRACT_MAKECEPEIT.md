# Prompt — Extract the Makecepeit build intelligence

Paste this prompt into the Claude conversation/project that contains the Makecepeit build history. If Claude has access to repository history/files as well, let it inspect them only when useful to understand decisions made in the chat.

---

I am building a reusable Claude Code SaaS Factory V0 based primarily on the lessons from how we built Makecepeit.

Your task is NOT to continue building Makecepeit and NOT to redesign it. Your task is to analyze the full available Makecepeit conversation/history and extract the reusable operating knowledge that should teach another Claude instance how I like simple SaaS products to be built.

## Important constraints
- Makecepeit is the PRIMARY source for this extraction.
- Extract what was actually learned during the build: my corrections, rejected approaches, accepted approaches, recurring requests, implementation mistakes, UX/SEO/content decisions, deployment issues, and final patterns.
- Do not convert one-off project facts into universal rules unless there is a clear general lesson.
- Distinguish explicit user preferences from your own inferred best practices.
- Do not preserve obsolete instructions that were later corrected.
- When two messages conflict, prefer the latest clearly accepted decision.
- Be concise. The purpose is to reduce future Claude token usage, not create a giant knowledge base.
- Do NOT copy the full conversation into the output.
- Do NOT invent rules that are not supported by the conversation.

## Our V0 factory has only these agents
1. orchestrator
2. builder
3. design
4. seo
5. content
6. qa-launch

The technical default is:
- Next.js + TypeScript
- Supabase
- Sanity for editable content
- GitHub
- Cloudflare

## Classify every useful lesson into one of these types

### A. GLOBAL RULE
A short durable instruction that should apply to most SaaS builds.
Example form:
`RULE: Do not add fake social proof to make a landing page look complete.`

### B. AGENT RULE
A durable instruction specific to one of the six agents.
Example:
`AGENT: design — Prefer one obvious primary action instead of multiple equal CTA styles.`

### C. SKILL / PROCEDURE
A repeatable multi-step technique worth teaching an agent.
Example:
`SKILL: seo — How to map a focused SaaS into product, use-case, comparison and editorial pages without creating thin pages.`

### D. ANTI-PATTERN
Something that caused bad results, wasted time, broke the product, or repeatedly annoyed me.

### E. ACCEPTANCE CRITERION
A test that tells us when work is actually complete.

### F. PROJECT-ONLY FACT
Useful to understand Makecepeit but should NOT enter the global SaaS Factory rules.

## Areas to inspect carefully
- how the product scope was kept simple or became unnecessarily complicated
- core product workflow
- Next.js implementation decisions
- Supabase schema/auth/storage/RLS decisions
- APIs/integrations
- environment variables/secrets
- UI/UX decisions and my reactions to designs
- mobile/responsive behavior
- landing page structure
- pricing/CTA decisions
- trust elements and fake/generic content
- SEO architecture
- GEO/AEO considerations
- metadata/schema/internal linking
- content strategy
- blog/content quality
- Sanity usage/content modeling/publishing
- performance
- errors, loading and empty states
- analytics if discussed
- testing and QA
- Git/GitHub workflow
- Cloudflare deployment
- bugs that revealed reusable engineering lessons
- places where Claude over-researched, over-explained, over-engineered or wasted tokens
- things I repeatedly asked Claude to stop doing
- things I explicitly liked and wanted repeated

## Output format

### 1. Executive extraction
Maximum 15 bullets: the strongest principles that define how I build SaaS products.

### 2. Global rules
Use a table:
| ID | Rule | Evidence/why learned | Confidence |

Confidence must be: HIGH / MEDIUM / LOW.
Only HIGH and strong MEDIUM items are candidates for automatic reuse.

### 3. Agent rules
Group under exactly:
- orchestrator
- builder
- design
- seo
- content
- qa-launch

For each rule include:
- rule
- why it exists
- HIGH/MEDIUM/LOW

### 4. Reusable skills/procedures
For each skill:
- skill name
- owner agent
- trigger: when to use it
- concise step-by-step procedure
- what NOT to do
- completion checks

Do not create a skill if the lesson is adequately expressed as one sentence rule.

### 5. Anti-patterns
For each:
- anti-pattern
- what happened / why it was bad
- replacement behavior

### 6. Acceptance criteria
Group by builder / design / seo / content / qa-launch.

### 7. Project-only facts to EXCLUDE from the factory
List Makecepeit-specific facts that should remain project memory and not become global rules.

### 8. Proposed factory file updates
Map every HIGH-confidence reusable item into one or more of these destinations:
- `CLAUDE.md` only for truly global high-level behavior
- `rules/product.md`
- `rules/design.md`
- `rules/engineering.md`
- `rules/seo-content.md`
- `rules/launch.md`
- `.claude/agents/orchestrator.md`
- `.claude/agents/builder.md`
- `.claude/agents/design.md`
- `.claude/agents/seo.md`
- `.claude/agents/content.md`
- `.claude/agents/qa-launch.md`
- `.claude/skills/builder/SKILL.md`
- `.claude/skills/design/SKILL.md`
- `.claude/skills/seo/SKILL.md`
- `.claude/skills/content/SKILL.md`
- `.claude/skills/qa-launch/SKILL.md`

### 9. Machine-transfer block
At the end, produce ONE fenced YAML block called `factory_learnings` with normalized entries using this schema:

```yaml
factory_learnings:
  - id: MK-001
    type: global_rule | agent_rule | skill | anti_pattern | acceptance_criterion
    agent: orchestrator | builder | design | seo | content | qa-launch | null
    title: "..."
    instruction: "..."
    rationale: "..."
    confidence: high | medium | low
    destination:
      - "rules/..."
    project_specific: false
```

Make this YAML concise enough that I can paste it into the SaaS Factory repository for another Claude instance to integrate.

Before finalizing, deduplicate similar lessons and remove generic software advice unless the Makecepeit experience specifically demonstrated why it matters for my factory.
