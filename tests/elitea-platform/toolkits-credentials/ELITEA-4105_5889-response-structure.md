---
id: ELITEA-4105
title: "[EliteaAI/elitea_issues#5889] ADO Toolkit: Response Structure with Image Content"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5889, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend]
requirements: [EliteaAI/elitea_issues#5889]
---

# ELITEA-4105: ADO Toolkit — Response Structure with Image Content

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that tool response includes image descriptions with clear separation from comment text.

## Preconditions

- ADO toolkit configured with `process_images: true`
- Comments with both text and images retrieved
- Image descriptions extracted via LLM

## Test Data

| Field | Expected Content |
|-------|-----------------|
| comment_text | Original comment text (unchanged) |
| images | Array of image descriptions |
| image.url | ADO image URL |
| image.description | LLM-extracted content |
| image.format | JPEG, PNG, GIF, WebP |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call get_comments with `process_images: true`. | Response includes both comment text and images. |
| 2 | Verify response has clear separation: comment text and image content in distinct fields. | Two separate sections in response. |
| 3 | Verify image description included alongside comment text (not replacing). | Original comment text preserved. |
| 4 | Verify metadata includes image URL. | URL included for traceability. |
| 5 | Verify metadata includes image format (JPEG, PNG, etc.). | Format type identified. |
| 6 | Verify metadata includes extraction timestamp (if applicable). | When image was processed. |
| 7 | Test response with multiple images: all descriptions present. | All image descriptions in response. |
| 8 | Test response backward compatibility: `process_images: false` produces only text. | No image section in response. |

## Expected Final State

- Response includes image descriptions alongside comment text
- Clear distinction between original comment and image content
- Metadata (URL, format, timestamp) included for each image
- Original comment text preserved (not modified)
- Response format backward compatible with `process_images: false`

## Pass/Fail Criteria

**Pass:** Image descriptions in response; clear separation from text; metadata included; backward compatible.  
**Fail:** Image content missing from response; text replaced/modified; metadata incomplete; backward compatibility broken.
