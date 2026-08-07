---
id: ELITEA-2608
title: "[EliteaAI/elitea_issues#5889] ADO Toolkit: Supported Image Formats (JPEG, PNG, GIF, WebP)"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5889, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend]
requirements: [EliteaAI/elitea_issues#5889]
---

# ELITEA-2579: ADO Toolkit — Supported Image Formats

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that all common image formats (JPEG, PNG, GIF, WebP) are successfully processed.

## Preconditions

- ADO toolkit configured with `process_images: true`
- Test images in multiple formats available in ADO work items
- LLM vision model supports all formats

## Test Data

| Format | Extension | Expected |
|--------|-----------|----------|
| JPEG | .jpg, .jpeg | Supported |
| PNG | .png | Supported |
| GIF | .gif | Supported (static) |
| WebP | .webp | Supported |
| Unsupported | .svg, .bmp | Error message |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call get_comments on work item with JPEG image. | JPEG downloaded successfully; content extracted. |
| 2 | Verify JPEG content extracted via LLM vision model. | LLM successfully analyzes JPEG; description returned. |
| 3 | Call get_comments on work item with PNG image. | PNG downloaded; content extracted. |
| 4 | Verify PNG content extracted via LLM. | LLM successfully analyzes PNG. |
| 5 | Call get_comments on work item with GIF image (static). | GIF downloaded; first frame analyzed. |
| 6 | Verify GIF content extracted. | GIF description returned. |
| 7 | Call get_comments on work item with WebP image. | WebP downloaded; content extracted. |
| 8 | Verify WebP content extracted via LLM. | LLM successfully analyzes WebP. |
| 9 | Test unsupported format (SVG): verify graceful error. | SVG rejected with clear message. |
| 10 | Test unsupported format (BMP): verify graceful error. | BMP rejected with clear message. |
| 11 | Test auto-format detection: verify correct handler applied. | Format identified correctly regardless of URL extension. |

## Expected Final State

- JPEG, PNG, GIF, WebP all supported
- Format auto-detection working
- Unsupported formats return clear errors
- All supported formats produce valid descriptions
- No blocking errors with unsupported formats

## Pass/Fail Criteria

**Pass:** All common formats supported; unsupported formats fail gracefully; auto-detection works.  
**Fail:** Any supported format fails; unsupported formats not rejected clearly; detection incorrect.
