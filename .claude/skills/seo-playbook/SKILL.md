---
name: seo-playbook
description: SaaS Factory SEO workflow — page/intent mapping, search-intent gate, when to stop on-page polish.
---

# SEO / GEO / AEO Skill

## Workflow
1. Use supplied positioning and keywords.
2. Map distinct intent to the minimum useful set of pages.
3. Implement technical essentials.
4. Add structured data only when it accurately represents visible content/product facts.
5. Improve answer clarity and entity/product context for GEO/AEO.
6. Build internal links intentionally.
7. Validate indexability and canonical behavior.

Never invent SEO metrics.

## Competitor page export (for the content agent)
Data source: DataForSEO (MCP `mcp__dataforseo__*`). Set `limit` on every call.
1. Confirm 3–5 competitors: owner-named first, otherwise `dataforseo_labs_google_competitors_domain` (or `serp_competitors` for the main keywords).
2. Per competitor, top pages by organic traffic: `dataforseo_labs_google_relevant_pages` (keywords, positions, estimated traffic, traffic value).
3. Conversion signals: paid keywords and their landing pages via `dataforseo_labs_google_ranked_keywords` with paid results, keyword intent via `dataforseo_labs_search_intent`, most-linked pages via `backlinks_domain_pages`.
4. Keyword gap: `dataforseo_labs_google_domain_intersection` (they rank, we don't).
5. Save dated raw responses in the project; reuse them instead of re-pulling.
6. Hand over one table: competitor · URL · page type · top keywords · intent · est. traffic · traffic value · paid ads (y/n) · referring domains. Do not decide the content plan — that's the content agent's job.

## Search-intent gate
1. Classify each keyword as retrieval (find a known thing), definition (what is X) or creation (make/do X).
2. Target creation intent first; retrieval and definition queries go on supporting pages only.
3. For a low-CTR page that ranks on page 1, compare its actual query list to its title/H1 before calling it "zero-click". It is often an intent mismatch, which is fixed by retitling or rewriting the page.

## When the crawl is clean
Once titles, meta, H1, canonical and schema show zero defects, stop on-page tweaking. Move effort to intent fixes, content depth and authority.
