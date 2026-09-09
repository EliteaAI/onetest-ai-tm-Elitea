---
id: ELITEA-3358
title: "PDF extra_params (page_number) Not Affected by Image Changes"
priority: critical
type: regression
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, feat:image-vision, r-2.0.6, parameter-isolation, regression]
requirements: [EliteaAI/elitea_issues#6530]
---
# ELITEA-3358: PDF extra_params (page_number) Not Affected by Image Changes

**Module:** Artifacts Toolkit Read File · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that PDF-specific `extra_params` (like `page_number`) still work correctly and don't conflict with the new image `user_prompt` parameter.

**Coverage:**
- PDF parameters isolated from image parameters
- No namespace collision
- PDF functionality unchanged

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `read_file` enabled
- `multi_page.pdf` with 5 pages in bucket `test`
  - Page 1: "Content of page 1"
  - Page 2: "Content of page 2"
  - Page 3: "Content of page 3"

## Test Data

| File | extra_params | Expected Result |
|---|---|---|
| multi_page.pdf | {"page_number": 2} | Content from page 2 only |
| multi_page.pdf | {"start_page": 1, "end_page": 2} | Content from pages 1-2 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file` on `multi_page.pdf` with `extra_params={"page_number": 2}`. | Tool executes successfully. |
| 2 | Verify response contains content from page 2 only. | Response includes "Content of page 2", not pages 1, 3, 4, or 5. |
| 3 | Call `read_file` on same PDF with `extra_params={"start_page": 1, "end_page": 2}`. | Tool executes successfully. Content from pages 1-2 returned. |
| 4 | Verify PDF parameters work as documented. | Page extraction works correctly with no interference from image parameter changes. |

## Expected Final State

PDF `extra_params` work exactly as before; no conflict with image `user_prompt` parameter.

## Pass/Fail Criteria

**Pass:**
- `page_number` extracts correct page
- `start_page`/`end_page` work correctly
- No parameter conflicts

**Fail:**
- PDF parameters fail after image enhancement
- Parameter namespace collision detected
- Unexpected behavior when using PDF-specific parameters
