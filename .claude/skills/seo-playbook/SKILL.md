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

## Semantic SEO & topical authority analysis
Question: which topics must the site own to be the trusted source for its core entity, and where is it weaker than competitors?
Data: DataForSEO, `limit` on every call, one market/language from PROJECT.md, dated raw responses saved and reused. Never invent scores — every number traces to a saved response.
1. **Central entity and source context.** From PROJECT.md: the product's core entity (e.g. "invoice"), the audience, and what the product legitimately does. Topics that don't connect to it are out of scope.
2. **Entity map.** Core entity → attributes (types, parts, steps, rules, costs, problems) → related entities (tools, roles, documents, regulations). Source the questions from `dataforseo_labs_google_keyword_ideas` / `related_keywords` and SERP People Also Ask (`serp_organic_live_advanced`). Apply the stay-legitimate rule.
3. **Topical map.** Cluster queries by SERP overlap (`seo-cluster`). Split into **core** clusters (creation intent, close to the product, links to signup) and **outer** clusters (definitions, comparisons, how-tos that feed the core). One hub per cluster, spokes only where intent is distinct.
4. **Coverage audit.** Map each node to an existing URL: covered / thin / cannibalized (2+ URLs for one intent) / missing. Use our `ranked_keywords` for real positions.
5. **Competitor coverage.** For the 3–5 competitors from the competitor export, count nodes each one covers per cluster (`relevant_pages`, `domain_intersection`). Report per cluster: nodes total · we cover · best competitor covers · our avg position · their avg position. That ratio is the topical-authority gap; state it as counts, not a made-up score.
6. **Semantic page check** (core hubs first). Compare each hub against the top 3 ranking pages (`on_page_content_parsing`): attributes and questions they answer that we don't, one consistent term per concept, H2/H3 following the entity → attribute order, direct first-sentence answers. JSON-LD `about`/`mentions` only for entities visible on the page.
7. **Internal links.** Hub ↔ spokes both ways, spoke → product page, contextual anchors naming the target entity; outer clusters link inward to core, not the reverse chain. Flag orphans and links that cross clusters without a reason.
8. **Hand-off.** One table in SEO.md "Topical map": cluster · core/outer · node · intent · URL or missing · status · competitor coverage · priority (core + missing + competitor-covered first). Content decides what to write; builder fixes links/schema.

## Search-intent gate
1. Classify each keyword as retrieval (find a known thing), definition (what is X) or creation (make/do X).
2. Target creation intent first; retrieval and definition queries go on supporting pages only.
3. For a low-CTR page that ranks on page 1, compare its actual query list to its title/H1 before calling it "zero-click". It is often an intent mismatch, which is fixed by retitling or rewriting the page.

## When the crawl is clean
Once titles, meta, H1, canonical and schema show zero defects, stop on-page tweaking. Move effort to intent fixes, content depth and authority.
