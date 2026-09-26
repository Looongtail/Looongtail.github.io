---
name: it-trend-publishing
description: "Create and finalize Korean IT Trend post files, including source-grounded editing, embedded local visual assets, and build verification. Use as the authoring stage before review/deploy; not for unrelated site development."
---

# IT Trend Authoring

Create a finished, publication-ready IT Trend post from a draft, research notes, or a user-supplied shared ChatGPT conversation. This is stage 1 of the three-stage chain: authoring → review/deploy → Google Docs upload. The post should explain why the topic matters to enterprise IT without presenting speculation as established fact.

Before every writing or substantive editing task, read [docs/RULES.md](docs/RULES.md). For a new article or a major restructuring, also read [docs/TEMPLATE.md](docs/TEMPLATE.md) and adapt it to the topic rather than copying every section mechanically.

## Project context

- Work from the repository in `codes/`; use `pnpm` there.
- Publish posts under `codes/src/content/posts/`. Match the `posts` collection schema in `codes/src/content.config.ts`: `title`, `description`, `pubDate`, `category`, and `slug` are required; use `tags` deliberately.
- Keep URLs trailing-slash compatible by using a stable, meaningful `slug`. Do not change an existing post's slug unless the user asks.
- Put local visual assets in `codes/public/images/contents/it-trend/<topic>/` and reference them in Markdown as `/images/contents/it-trend/<topic>/<filename>`.
- Treat `codes/writing/` as a draft workspace. Do not move or delete a user draft unless the user asks to publish that specific draft.

## Editorial workflow

1. Inspect the closest published IT Trend posts and the supplied draft before choosing the article structure. When the user supplies a completed prior article or shared-conversation text, treat it as the baseline: make a checklist of its thesis, sections, company context, tables, visuals, conclusions, and sources, then verify that substantive editing has not silently removed or generalized them. Preserve the user's intended thesis and distinguish factual reporting, analysis, and recommendations.
2. Research claims that may be current, contested, numerical, or specific to a company/product. Prefer primary sources and cite compactly in a final `## 출처` section. Do not invent sources, case studies, product capabilities, survey findings, or figures.
3. Write in natural Korean with an analytical, enterprise-IT focus. Open with the practical change or decision at stake, use conclusion-led section headings, and explain technical terms only when they affect the argument. Avoid promotional language and unqualified predictions.
4. Use tables only when they make comparisons or choices easier to scan. Explain the point of a table in the surrounding prose.
5. Keep the article's scope honest: label inferred applications as possibilities, and state material limits, trade-offs, or validation needs.

## Visual assets

Add an image only when it makes a relationship or process materially clearer than text.

- For original conceptual diagrams, flows, or editorial illustrations, use ImageGen. Keep the visual purposeful, avoid embedded body text that must be exact, save the resulting asset under the post's image directory, and add an accurate Korean caption.
- For web-sourced images, use only assets with clear reuse rights or an explicit user instruction to use that source. Record the source and license/permission in the article's sources or adjacent caption as appropriate; do not hotlink external image URLs.
- Preserve aspect ratio, descriptive alt text, and a consistent restrained editorial style. Do not use decorative stock imagery merely to fill space.

## Completion checks

- Re-read the final Markdown for frontmatter validity, heading flow, claim/source alignment, Korean typography, asset paths, and links.
- Run `pnpm build` in `codes/` after editing. Fix errors caused by the change; do not alter unrelated work or delete untracked drafts/assets.
- Report the created or changed post and visual assets, the verification result, and any claims that still need the user's source or approval.
- Do not commit, push, deploy, or create a Google Doc in this stage. Hand the exact post and asset paths to the next applicable stage.
