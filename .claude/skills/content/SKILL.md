---
name: content
description: SaaS Factory content procedures — competitive content plan from competitor pages (traffic + conversion signals), content/tool briefs, Sanity workflow and scheduled publishing batches.
---

# Content + Sanity Skill

## Competitive content plan
1. Get the competitor page export from the seo agent (3–5 competitors; their top pages by traffic, plus paid landing pages and most-linked pages).
2. Classify each competitor page by type: blog, free tool/calculator, comparison/alternatives, template/example, use-case/industry, glossary, docs/help, landing.
3. Score each page:
   - **Traffic** (measured): estimated organic visits and traffic value (visits × CPC).
   - **Conversion signal** (estimated, never measured): high if it is a paid-ads landing page, targets commercial/transactional or creation keywords, or has a strong product CTA/tool-to-signup path; medium if it's informational with a product CTA; low otherwise.
4. Group by type to see which page types drive both traffic and conversion for the competitors.
5. For each opportunity, decide: create, improve an existing page, or skip (apply rules/seo-content.md: demand, distinct intent, legitimacy, no per-variant padding).
6. Prioritize: high traffic + high conversion signal first; free tools and comparison pages usually lead for SaaS when they fit the core action.
7. Write the plan into CONTENT.md (template table) with an owner per item: content (articles/guides), marketing (conversion pages), builder + design (free tools).
8. For each accepted item, write a brief: target query and intent, competitor page to beat and why it wins, our angle, outline, CTA to the product, internal links.

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
