# Prompt — Fill the SaaS Factory files from extracted learnings

Run this from Claude Code while the working directory is the `saas-factory-v0` repository/folder. Save the outputs from prompts 01 and 02 in `/imports`, or paste them when asked.

---

We are updating the SaaS Factory V0 with lessons extracted from Makecepeit and PayDocs.

Read:
- `CLAUDE.md`
- `README.md`
- `.claude/agents/*.md`
- `.claude/skills/*/SKILL.md`
- `rules/*.md`
- all relevant extraction files in `imports/`

Makecepeit is the primary source. PayDocs is secondary and should confirm, refine, challenge, or extend Makecepeit lessons.

## Task
Integrate the extracted learnings directly into the existing factory files.

## Critical rules
- Keep this a SMALL V0.
- Do NOT create new agents unless absolutely unavoidable. The six agents remain:
  orchestrator, builder, design, seo, content, qa-launch.
- Do NOT make separate frontend/backend/database/Sanity agents.
- Sanity belongs to the content agent when publishing content; technical Sanity integration can be implemented by builder when necessary.
- UX/UI/frontend visual design belong to design.
- Normal Next.js/Supabase/API/integration engineering belongs to builder.
- QA/security sanity/release/deployment checks belong to qa-launch.
- Do NOT copy chat transcripts into the factory.
- Do NOT add low-confidence rules as mandatory behavior.
- Do NOT duplicate the same rule in many files unless the short duplication is necessary for agent execution.
- Do NOT turn one project-specific choice into a global default without justification.
- Resolve newer accepted corrections over older instructions.
- If Makecepeit and PayDocs conflict, formulate the narrowest correct conditional rule rather than picking one blindly.
- Optimize for Claude token efficiency. Concise operational instructions beat essays.

## Placement policy
Use `CLAUDE.md` only for:
- system mission
- global workflow/efficiency behavior
- stack defaults
- definition of done
- cross-agent principles

Use `rules/*.md` for durable reusable product/build rules.

Use `.claude/agents/*.md` for role-specific behavior and boundaries.

Use `.claude/skills/*/SKILL.md` only for repeatable multi-step procedures/checklists. A one-sentence preference is a rule, not a skill.

## Integration process
1. Parse and deduplicate all learnings.
2. Ignore `project_specific: true` items.
3. Identify contradictions.
4. Prefer high-confidence evidence.
5. Convert repeated corrections into short explicit rules.
6. Convert repeated successful workflows into skills only where useful.
7. Edit the files directly.
8. Keep the total instruction footprint compact.
9. After editing, audit for contradictions and duplicated instructions.
10. Produce a short change summary.

## Final report
Tell me only:
- files changed
- strongest rules added
- contradictions resolved
- learnings deliberately excluded and why
- any rule you believe requires my manual decision

Do not start changing the actual Makecepeit or PayDocs products. This task changes only the SaaS Factory V0.
