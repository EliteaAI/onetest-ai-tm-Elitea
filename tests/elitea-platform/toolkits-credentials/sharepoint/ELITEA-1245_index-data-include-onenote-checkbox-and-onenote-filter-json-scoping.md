---
id: ELITEA-1245
title: "Index data: \"Include Onenote\" checkbox and Onenote Filter JSON scoping"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2355, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2355]
---
# ELITEA-1245: Index data: "Include Onenote" checkbox and Onenote Filter JSON scoping

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that the "Include Onenote" checkbox and Onenote Filter JSON correctly scope what OneNote content is indexed, including notebook/section granularity, image/attachment capture flags, and invalid JSON handling.

**Coverage:**
- "Include Onenote" unchecked excludes OneNote from indexing
- Empty filter `{}` indexes all notebooks
- Notebook-scoped filter indexes only the specified notebook
- Section-scoped filter indexes only the specified section
- `capture_images` and `include_attachments` flags respected during indexing
- Invalid JSON in filter returns a clear error

## Preconditions

- SharePoint toolkit configured with Delegated OAuth auth and valid credentials
- Agent with SharePoint toolkit attached
- SharePoint site has at least one OneNote notebook with content and at least one non-OneNote document
- Notebook ID and Section ID values retrieved in advance via Onenote get notebooks / Onenote get sections

## Test Data

- Filter — all content: {}
- Filter — specific notebook (all sections): {"notebooks": [{"id": "<notebook_id>"}]}
- Filter — specific section only: {"notebooks": [{"id": "<notebook_id>", "sections": [{"id": "<section_id>"}]}]}
- Filter — with images & attachments: {"capture_images": true, "include_attachments": true}
- Invalid filter: {invalid json

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `Index data` with "Include Onenote" unchecked. Run `Search index` with a keyword present only in OneNote content. | Search returns no OneNote results — OneNote was excluded from indexing. |
| 2 | Invoke `Index data` with "Include Onenote" checked, Onenote Filter `{}`. | Indexing completes without errors. All notebooks on the site are indexed. |
| 3 | Run `Search index` with a keyword present in an indexed OneNote page. | Matching OneNote page(s) are returned. |
| 4 | Invoke `Index data` with filter {"notebooks": [{"id": "<notebook_id>"}]}. Run `Search index` with a keyword from a different notebook. | No results from the excluded notebook — only the specified notebook was indexed. |
| 5 | Invoke `Index data` with filter {"notebooks": [{"id": "<notebook_id>", "sections": [{"id": "<section_id>"}]}]}. Run `Search index` with a keyword from a page in a different section of the same notebook. | No results from the excluded section — only the specified section was indexed. |
| 6 | Invoke `Index data` with filter {"capture_images": true, "include_attachments": true}. | Indexing completes. Images and file attachments from OneNote pages are included in indexed content. |
| 7 | Invoke `Index data` with Onenote Filter set to `{invalid json`. | A clear error is returned indicating invalid JSON. Indexing does not proceed. |

## Expected Final State

A clear error is returned indicating invalid JSON. Indexing does not proceed.

## Pass/Fail Criteria

**Pass:**
- Checkbox and all filter options correctly scope indexing
- `capture_images`/`include_attachments` flags respected
- Invalid JSON returns clear error

**Fail:**
- Filter scope ignored
- Invalid JSON causes silent failure or crash
