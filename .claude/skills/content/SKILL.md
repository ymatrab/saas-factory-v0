---
name: content
description: SaaS Factory content + Sanity workflow and scheduled publishing batches.
---

# Content + Sanity Skill

## Workflow
1. Read accepted product/SEO context.
2. Plan only if no accepted plan exists.
3. Write specific, factual copy in the accepted messaging voice (PROJECT.md "Messaging & conversion").
4. Match each search page to its intended query/user need.
5. Use Sanity for content intended to be maintained editorially.
6. Respect existing schemas; change schemas only when the content model genuinely needs it.
7. After publishing, verify slug, metadata, references, portable text/content shape and frontend rendering.

## Scheduled publishing batch
1. Validate each keyword against the intent gate and the legitimacy rule (rules/seo-content.md).
2. Dry-run the publish script first.
3. Use deterministic, idempotent document ids so a re-run updates instead of duplicating.
4. Spread future `publishedAt` dates across the batch; avoid bulk drops on one day.
5. Update the ledger in CONTENT.md as each item is written.
6. Confirm sitemap and IndexNow pick up the published items.
7. Leave the most recently published posts (~20) untouched until they have been indexed and measured.
