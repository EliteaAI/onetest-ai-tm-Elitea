---
id: ELITEA-2571
title: "[EliteaAI/elitea_issues#5889] ADO Toolkit: Image Detection (HTML tags & Attachments)"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5889, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend]
requirements: [EliteaAI/elitea_issues#5889]
---

# ELITEA-2571: ADO Toolkit — Image Detection (HTML tags & Attachments)

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the toolkit correctly detects images from both HTML img tags and ADO attachment metadata in comments.

## Preconditions

- ADO toolkit configured with `process_images: true`
- Logged into agent/pipeline that uses ADO toolkit
- ADO work item has comments with:
  - Inline HTML `<img>` tags pointing to image URLs
  - Attachment metadata with image URLs
  - Non-image attachments (docs, PDFs, etc.)
- Comments contain both image and text content

## Test Data

| Type | Content | Expected |
|------|---------|----------|
| HTML img tag | `<img src="http://ado-url/image.jpg">` | Detected |
| Attachment | Image URL from metadata | Detected |
| Non-image attachment | PDF, DOCX, TXT | Filtered out |
| Comment with no images | Text only | Skipped gracefully |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call get_comments with `process_images: true` on work item with mixed content. | Tool returns comment list. |
| 2 | Verify tool detects HTML `<img>` tags in comment HTML. | Image URLs extracted from HTML tags. |
| 3 | Verify tool detects ADO attachment metadata with image URLs. | Image URLs from attachment metadata identified. |
| 4 | Verify non-image attachments (PDF, DOCX, etc.) are filtered out. | Only image attachments included; others skipped. |
| 5 | Verify comments with no images are handled gracefully. | Processing continues without error; no false positives. |
| 6 | Verify both HTML and attachment images detected in single comment. | All image sources processed in one call. |
| 7 | Verify image detection works with multiple comments (5+). | All images across comments detected. |
| 8 | Verify edge case: HTML img with malformed URL is skipped gracefully. | Malformed URL logged but doesn't block other images. |

## Expected Final State

- HTML `<img>` tags detected in comment HTML
- ADO attachment image URLs detected
- Non-image attachments filtered out
- Comments without images handled gracefully
- Both HTML and attachment images processed in single call
- Multiple comments processed without blocking

## Pass/Fail Criteria

**Pass:** All image sources detected; non-images filtered; no blocking; graceful handling of edge cases.  
**Fail:** Images missed; non-images included; processing blocked by malformed URLs; inconsistent detection.
