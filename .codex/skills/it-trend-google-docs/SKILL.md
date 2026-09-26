---
name: it-trend-google-docs
description: "Create a native Google Docs edition of an already published IT Trend post, with its local images embedded and verified in the designated Drive folder. Use as the final stage after it-trend-review-deploy; not for article authoring or website deployment."
---

# IT Trend Google Docs Upload

Use this as stage 3 of the IT Trend chain, only after `it-trend-review-deploy` has successfully deployed the intended post. Create a native Google Docs edition from the deployed post's Markdown and local assets; do not re-author, summarize, or silently alter the article.

Before starting, read [`../it-trend-publishing/docs/RULES.md`](../it-trend-publishing/docs/RULES.md) and [`docs/UPLOAD_NOTES.md`](docs/UPLOAD_NOTES.md). Use the `documents`, `google-drive`, and `google-docs` skills for the document-generation and Drive operations.

## Inputs and scope

- Identify the exact published Markdown file, its public URL, and every locally referenced image. Treat that Markdown as the source of truth for title, body, tables, captions, and `## 출처`.
- Keep all article content, including company-specific context, tables, captions, and source list. Correct only a demonstrated conversion defect, and report it.
- The target is a new native Google Doc in Drive folder `1upNwdQ9E-tj9OiSFgNvfYo5PlR13gD7x`. Set the Drive file title to `[yyyy-mm-dd] <article title>`, using the post's `pubDate` in ISO date form (for example, `[2026-09-27] Rust의 부상: 기업 IT 인프라와 데이터센터를 위한 새로운 언어 선택`). Do not overwrite an existing Google Doc unless the user explicitly identifies it.

## Creation and verification

1. Build an import-ready DOCX/HTML staging artifact with the Google Docs format in `RULES.md`, explicitly setting A4 and 72pt margins. Embed each local post image as an inline image; do not leave image paths, remote hotlinks, or captions without their image.
2. For Korean text, specify an appropriate East Asian fallback font in addition to Arial. A local DOCX/PDF renderer may lack Korean glyphs, so do not mistake its missing glyphs for lost source text; verify the imported native Doc's text after conversion.
3. Import as `native_google_docs` into the designated folder. Confirm the resulting file has Google Docs MIME type and the expected parent folder.
4. Read back the native document. Confirm title, all sections, tables, captions, image positions/count, and `## 출처`; use `get_document` to check inline objects rather than inferring images from captions alone. Ensure the article is not a shortened or plain-text-only conversion. Use a concrete date chip for the date metadata when the connector supports it, then read back the resulting document.
5. Export or otherwise inspect the native document when practical for visual QA. If the connector cannot expose a rendered page, report that constraint rather than claiming visual inspection. Keep temporary source artifacts only until the native-document checks have passed, then remove only the explicit temporary staging directory.

## Handoff report

Report the Google Docs URL, that it is native (not an attached DOCX), its folder placement, the verified image count, and any conversion limitation. Do not commit, change the published site, or alter unrelated files in this stage.
