# SaaS Factory V0 for Claude Code

A lightweight, project-scoped multi-agent SaaS builder for simple commercial SaaS products.

## Goal
Give Claude Code a concise SaaS brief and have it help build the actual product — not spend most of the session validating whether the idea should exist.

Default stack:
- Next.js / TypeScript
- Supabase
- Sanity
- GitHub
- Cloudflare

## Why this folder is isolated
Keep this folder/repository separate from your global Claude Code configuration. `CLAUDE.md`, `.claude/agents`, `.claude/skills`, rules, prompts, and templates are all scoped to this SaaS Factory project.

## Seven V0 agents
- orchestrator
- builder
- marketing (sales, copy, conversion — before design)
- design
- seo
- content
- qa-launch

This is intentionally small to reduce token consumption on a Claude subscription.

## Suggested setup
1. Unzip this folder.
2. Open this folder itself in Claude Code when you want the factory.
3. Add or clone the target SaaS into a project workspace, or adapt the structure to your preferred repo workflow.
4. Fill `PROJECT.md` from the template.
5. Use the prompts in `/prompts` to extract the best reusable rules from your Makecepeit and PayDocs build chats.
6. Review the extracted rules before accepting them.
7. Put accepted rules into `/rules` and detailed repeatable procedures into the relevant skill folders.

## Typical command to Claude
Example:

> We are building a new SaaS. Read CLAUDE.md and the project files. Here is the final product brief: [brief]. Create a concise implementation plan, then execute it using the minimum agents required. Do not revalidate the business idea. Keep the app simple, commercial, production-ready, SEO-ready, and optimized for the default stack.

## Important: learning from old chats
Do not paste old conversations into CLAUDE.md wholesale. Use the extraction prompts in `/prompts` to convert them into:
- concise durable rules
- agent-specific rules
- repeatable skills/checklists
- anti-patterns
- acceptance criteria

The Makecepeit extraction should be treated as the primary source and PayDocs as a second source for comparison and generalization.

## Folder map
```
saas-factory-v0/
├── CLAUDE.md
├── README.md
├── factory.config.yaml
├── .claude/
│   ├── agents/
│   └── skills/
├── rules/
├── prompts/
├── templates/
└── projects/
```

## Recommended learning cycle
Build → notice what worked/failed → extract rule → review → save rule/skill → use on next SaaS.

This is how the V0 becomes your own SaaS-building system without making every Claude session expensive.
