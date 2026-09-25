---
name: zotero-paper-workflows
description: "Run ordered Zotero research workflows: discover and archive source papers, then translate explicitly selected English PDFs into page-aligned Chinese PDFs and attach them under the matching Zotero items. Use when the user asks for this Zotero-paper pipeline or an extension of it."
---

# Zotero Embodied Paper Workflows

This skill defines an extensible, ordered workflow registry. Execute requested workflows in numeric order; do not skip an earlier workflow when a later one depends on its artifacts.

## Workflow registry

1. Read [workflow-1-zotero-ingest.md](references/workflow-1-zotero-ingest.md) when the user asks to search for papers, obtain PDFs, create or complete Zotero items, or archive original PDFs.
2. Read [workflow-2-pdf-translation.md](references/workflow-2-pdf-translation.md) when the user explicitly asks to translate PDFs under specified Zotero items and attach Chinese PDFs for comparison.

Future workflows should be added as `3`, `4`, and so on in this section, with one focused reference file per workflow. Preserve the numeric order and state dependencies between workflows.

## Shared operating rules

- Treat the user's named collection, item keys, titles, or selection criteria as the scope. Do not silently broaden the paper set.
- Keep original PDFs immutable. Store working copies and generated files separately from originals.
- Use the Zotero skill for library discovery and item relationships, and the PDF skill for PDF inspection, rendering, creation, and visual QA. Read those skills before performing the corresponding work.
- Before any external mutation—creating Zotero items, downloading files into the library, or adding attachments—report the intended scope and use only sources and destinations within that scope.
- Never bypass a paywall, fabricate a bibliographic record, or treat a search-result snippet as the paper PDF. Prefer publisher, repository, DOI landing pages, or openly licensed copies.
- Maintain a manifest mapping each parent Zotero item key to its source PDF, translated PDF, page count, page size, and attachment key when available.
- “Full translation” means no omitted body prose and no summary substitution. References, equations, code, numeric table values, and text embedded inside figures/charts may remain in the original language when the user explicitly allows them; label that choice in the manifest.
- Before reporting completion, verify the actual files, page counts, page dimensions, rendered layout, and Zotero parent-child relationships. If any requirement is unverified, report the gap instead of claiming completion.
