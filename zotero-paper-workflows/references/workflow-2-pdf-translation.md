# Workflow 2 — Translate selected PDFs and attach page-aligned Chinese copies

Use this workflow only when the user explicitly identifies the Zotero items or collection and asks for Chinese PDF translations. This workflow depends on Workflow 1's source manifest, but it can also start from already verified Zotero attachments.

## 1. Preflight and translation contract

1. Resolve the exact parent item keys and source PDFs. Count them; do not infer “all” from a partial search result.
2. For every source, record page count, page dimensions, rotation, crop boxes, and whether the page contains selectable text, scanned text, figures, tables, equations, or code.
3. Create a terminology glossary for the project. Keep technical terms consistent across papers; preserve established acronyms and give the Chinese expansion on first use where appropriate (for example, vision-language-action, VLA).
4. Translate the complete body prose page by page. Do not replace a page or section with a summary, abstract, or invented compression merely because the Chinese text is longer.

## 2. Preserve the comparison layout

1. Keep the original page count, page dimensions, rotation, page numbers, margins, column structure, and figure/table geometry.
2. Preserve the original figure and chart images and all English text embedded inside them. Preserve table values, equation glyphs, code, and model/dataset identifiers unless the user explicitly requests otherwise.
3. Text outside figures and tables may be translated, including headings and captions, but keep labels and references stable enough for side-by-side comparison. If a caption is part of a figure image, leave it unchanged.
4. Replace or overlay prose within the original text regions. If Chinese text does not fit, adjust the local font size or line spacing inside that region; do not move text into another page or alter neighboring figures.
5. For scanned pages, OCR the prose first and visually inspect the OCR before translation. Never erase a figure or table while removing an OCR/text layer.
6. Use the PDF skill's artifact-operation marker immediately before creating or modifying each final PDF. Render representative pages with Poppler or an equivalent renderer and inspect them visually.

## 3. File and attachment conventions

1. Keep the original source in `output/pdf/original/` and write the translated copy to `output/pdf/chinese/` using a name containing the parent key, for example `<item-key>_<short-title>_中文译文.pdf`.
2. Do not overwrite the source PDF. Keep draft and render-test PDFs under `tmp/` and never attach drafts.
3. Attach the final translated PDF as a child attachment of the matching parent item. Do not create an orphan item, a second bibliographic parent, or a detached attachment.
4. Before writing Zotero's database, close Zotero normally, create a timestamped database backup, and use an idempotent operation that detects an existing attachment before inserting another. Never force-kill Zotero to acquire the database lock.

## 4. Quality gates

For each translated PDF, verify:

- page count equals the source;
- page dimensions and rotation equal the source;
- page numbers remain aligned;
- every body-text page has Chinese translation rather than a summary or accidental untouched English prose;
- figure/chart/table internals remain unchanged in English;
- formulas, code, citations, and numeric values were not corrupted;
- rendered samples from title/abstract, dense two-column text, figure/table pages, equations, and final body pages are legible;
- the final file opens and has a deterministic hash.

For Zotero, verify:

- exactly one final translated attachment exists for each requested parent;
- every attachment path exists and opens;
- every child attachment's `parentItemID` points to the intended parent;
- no draft, abstract-only translation, duplicate, or orphan attachment was added;
- the manifest records parent key, child key, final path, page count, and verification result.

If a gate fails, keep the goal active and report the specific failing paper/page. Do not call the entire workflow complete because a smaller subset passed.
