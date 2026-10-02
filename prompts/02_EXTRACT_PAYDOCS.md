# Prompt — Use PayDocs to confirm, challenge and extend the rules

Paste this prompt into the Claude conversation/project that contains the PayDocs build history.

---

I am building a Claude Code SaaS Factory V0. I already extracted the primary rules from Makecepeit. PayDocs is the SECOND source: use it mainly to confirm, challenge, refine, or add missing reusable lessons.

Analyze the full available PayDocs build conversation/history.

## Goal
Do NOT create a second independent giant rule set. Instead identify:
1. lessons that independently CONFIRM likely Makecepeit rules
2. lessons that CONTRADICT or require exceptions to them
3. genuinely NEW reusable lessons absent from a typical Makecepeit-style build
4. PayDocs-only facts that must remain project-specific

## Factory agents
- orchestrator
- builder
- design
- seo
- content
- qa-launch

## Stack baseline
- Next.js + TypeScript
- Supabase
- Sanity when useful
- GitHub
- Cloudflare

## Extraction rules
- prefer latest accepted decisions
- distinguish user preference from Claude suggestion
- do not turn a one-off implementation into a global rule without a reusable reason
- do not include generic advice unless the PayDocs experience demonstrates it mattered
- keep output concise
- explicitly flag contradictions instead of silently merging them

## Output

### 1. Confirmations
Rules/patterns strongly reinforced by PayDocs.

### 2. Contradictions / exceptions
For each:
- candidate rule being challenged
- PayDocs evidence
- recommended more precise rule

### 3. New reusable lessons
Classify each as:
- GLOBAL RULE
- AGENT RULE
- SKILL / PROCEDURE
- ANTI-PATTERN
- ACCEPTANCE CRITERION

### 4. Project-only facts to exclude

### 5. Proposed updates to the same factory files
Use the destination list from the Makecepeit extraction if known; otherwise use:
- CLAUDE.md
- rules/*.md
- .claude/agents/*.md
- .claude/skills/*/SKILL.md

### 6. Machine-transfer block
Return one concise YAML block:

```yaml
factory_learnings:
  - id: PD-001
    relation: confirms | refines | contradicts | new
    related_makecepeit_rule: "MK-..." # null when unknown/new
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

Be conservative: a small number of high-quality lessons is better than repeating everything we did while building PayDocs.
