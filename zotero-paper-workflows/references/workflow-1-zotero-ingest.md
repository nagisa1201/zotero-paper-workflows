# Workflow 1 — Discover, download, and archive papers in Zotero

Use this workflow when the user wants a paper set found, downloaded, and represented in Zotero with the original PDFs attached.

## 1. Establish scope

1. Identify the target Zotero library and collection. Resolve the collection by name and key; do not assume that a similarly named collection is the target.
2. Derive the paper list from the user's criteria (for example, a topic plus a publication-date window). Record the selection rule and the final count before downloading.
3. For each candidate, deduplicate by DOI, arXiv ID, publisher identifier, or normalized title plus first author/year. Keep a record of excluded duplicates and why.

## 2. Retrieve authoritative metadata and PDFs

1. Prefer, in order: an existing Zotero attachment; a publisher or society PDF; an institutional repository; an arXiv or other author-posted open-access copy; a legally accessible archive copy.
2. Use the paper's DOI, title, authors, venue, and year to confirm identity. Do not use a search snippet, a review, or a different version as the source without recording the distinction.
3. Download the PDF to a deterministic staging location such as `output/pdf/original/<item-key>_<short-title>.pdf`. Preserve the original bytes and compute a hash.
4. If a paper cannot be legally retrieved, stop for that paper and report the exact missing source or ask the user for a PDF. Do not silently substitute a summary or an unrelated version.

## 3. Create or complete the Zotero record

1. Create or update the bibliographic item using authoritative metadata. Preserve an existing item when it matches; do not create duplicates merely because a PDF was found elsewhere.
2. Place the item in the requested collection and preserve its existing tags, notes, and attachments.
3. Attach the original PDF as a child attachment of that item. Prefer Zotero-managed storage when the library is configured for it; otherwise use a clearly recorded linked attachment. Never leave the source as an unrelated orphan attachment.
4. Use a stable attachment title such as `Full Text PDF` or the source filename and retain the DOI/URL in the item metadata when available.

## 4. Verify before handing off to Workflow 2

For every selected item, verify:

- the parent item key and title match the intended paper;
- the source PDF exists and opens;
- the PDF page count and page dimensions are recorded;
- the attachment is a child of the correct parent;
- the downloaded file hash and source URL are in the manifest;
- no duplicate parent or duplicate source attachment was created.

Only after this evidence exists should Workflow 2 begin.
