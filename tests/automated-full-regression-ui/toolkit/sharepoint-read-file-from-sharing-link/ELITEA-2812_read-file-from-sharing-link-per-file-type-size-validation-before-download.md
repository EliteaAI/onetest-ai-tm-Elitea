---
id: ELITEA-2812
title: "Regression - read_file_from_sharing_link Per-File-Type Size Validation Before Download"
priority: critical
type: regression
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:toolkits, issue:6051, file-size-validation, image-limit, pre-download-validation, read_file_from_sharing_link]
requirements: [EliteaAI/elitea_issues#6051]
---
# ELITEA-2812: Regression - read_file_from_sharing_link Per-File-Type Size Validation Before Download

**Module:** Sharepoint · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that `read_file_from_sharing_link` validates file size against the correct cap for each file type before downloading/parsing — 20MB for non-image documents, 3MB for images.

## Preconditions

- SharePoint Delegated credential is connected and authenticated
- Sharing links are available for each of the two test files below

## Test Data

| File | Type | Size | Expected Cap Applied |
|------|------|------|----------------------|
| Large document | Non-image document (e.g. `.docx`/`.pdf`) | > 20MB | 20MB document limit |
| Large image | `.png` or `.jpg` | > 3MB | 3MB image limit |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file_from_sharing_link` on the sharing link of the non-image document (> 20MB) | Rejected immediately; error message references the file name and the ~20MB limit; no content is parsed |
| 2 | Call `read_file_from_sharing_link` on the sharing link of the image (> 3MB) | Rejected; error message specifically references the 3MB image limit (not the 20MB document limit) |

## Expected Final State

Each file type is validated against its correct pre-download size cap: oversized non-image documents and oversized images are both rejected with type-appropriate error text.

## Pass/Fail Criteria

**Pass:**
- Non-image document > 20MB is rejected with a message referencing the file name and the 20MB limit
- Image > 3MB is rejected with a message referencing the 3MB image limit

**Fail:**
- Either file type's rejection message references the wrong limit
- Either file is accepted despite exceeding its applicable cap
