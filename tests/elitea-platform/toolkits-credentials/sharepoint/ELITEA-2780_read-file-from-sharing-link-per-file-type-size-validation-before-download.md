---
id: ELITEA-2780
title: "read_file_from_sharing_link Per-File-Type Size Validation Before Download"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:toolkits, issue:6051, file-size-validation, image-limit, svg, pre-download-validation]
requirements: [EliteaAI/elitea_issues#6051]
---
# ELITEA-2780: read_file_from_sharing_link Per-File-Type Size Validation Before Download

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that `read_file_from_sharing_link` validates file size against the correct cap for each file type before downloading/parsing — 20MB for non-image documents, 3MB for images — and that SVG files (which are images by MIME type but are treated by the tool's own contract like a document) are not incorrectly rejected under the 3MB image cap.

## Preconditions

- SharePoint Delegated credential is connected and authenticated
- Sharing links are available for each of the three test files below

## Test Data

| File | Type | Size | Expected Cap Applied |
|------|------|------|----------------------|
| Large document | Non-image document (e.g. `.docx`/`.pdf`) | > 20MB | 20MB document limit |
| Large image | `.png` or `.jpg` | > 3MB | 3MB image limit |
| Large SVG | `.svg` | > 3MB but < 20MB | Document-class limit (not the 3MB image limit) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file_from_sharing_link` on the sharing link of the non-image document (> 20MB) | Rejected immediately; error message references the file name and the ~20MB limit; no content is parsed |
| 2 | Call `read_file_from_sharing_link` on the sharing link of the image (> 3MB) | Rejected; error message specifically references the 3MB image limit (not the 20MB document limit) |
| 3 | Call `read_file_from_sharing_link` on the sharing link of the SVG (> 3MB, < 20MB) | Accepted — not rejected as an oversized image; the SVG is processed under the document-class limit |

## Expected Final State

Each file type is validated against its correct pre-download size cap: oversized non-image documents and oversized images are both rejected with type-appropriate error text, while an SVG larger than 3MB (but under 20MB) is accepted rather than being misclassified as an oversized image.

## Pass/Fail Criteria

**Pass:**
- Non-image document > 20MB is rejected with a message referencing the file name and the 20MB limit
- Image > 3MB is rejected with a message referencing the 3MB image limit
- SVG > 3MB and < 20MB is accepted

**Fail:**
- SVG is incorrectly rejected under the 3MB image cap
- Any file type's rejection message references the wrong limit (e.g. document rejected citing the 3MB image limit, or vice versa)
