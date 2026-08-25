---
id: ELITEA-2727
title: "File breadcrumb navigation works correctly"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- HTML file is in nested folder structure

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Bucket | Elitea S3 storage |
| Path | html-htm > script > test_file_2_between_1_3mb_structured.htm |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Artifacts | Artifacts page loads |
| 2 | Select "Elitea S3 storage" bucket | Bucket contents display |
| 3 | Navigate to html-htm > script folder | Folder contents display |
| 4 | Open test_file_2_between_1_3mb_structured.htm | File opens in Canvas |
| 5 | Observe breadcrumb in Canvas header | Breadcrumb shows path |
| 6 | Verify path shows full hierarchy | Path is complete |
| 7 | If breadcrumb is clickable, click on a folder segment | Navigation occurs (optional) |

## Expected Final State

- Breadcrumb shows: html-htm > script > [filename]
- Path is clear and readable
- Breadcrumb helps user understand file location

## Pass/Fail Criteria

**Pass:**
- Breadcrumb displays in Canvas header
- Path shows correct hierarchy
- Path is clear and readable
- Helps user understand file location

**Fail:**
- No breadcrumb displayed
- Path is incomplete or incorrect
- Path is unreadable or confusing
- Breadcrumb shows wrong location
