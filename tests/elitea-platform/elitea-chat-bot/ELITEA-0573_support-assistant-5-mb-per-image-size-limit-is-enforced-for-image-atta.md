---
id: ELITEA-0573
title: "Support Assistant — 5 MB Per-Image Size Limit Is Enforced for Image Attachments; SVG Is Exempt"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0573: Support Assistant — 5 MB Per-Image Size Limit Is Enforced for Image Attachments; SVG Is Exempt

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify image files exceeding 5 MB are rejected with a clear error, images at or below 5 MB are accepted, SVG files are exempt from the 5 MB limit, and non-image files > 5 MB are accepted.

**Coverage:**
- Image at exactly 5 MB: accepted
- Image slightly above 5 MB (5.1 MB): rejected with clear error
- SVG > 5 MB: accepted (SVG exempt)
- Non-image file > 5 MB (e.g., 10 MB PDF): accepted

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin
- Browser: Chrome/Edge (latest)
- Test files: image_5mb_exact.png (exactly 5 MB), image_5.1mb.png (5.1 MB), large.svg (> 5 MB), large_document.pdf (> 5 MB)

## Test Data

| File | Size | Expected Outcome |
|---|---|---|
| image_5mb_exact.png | Exactly 5 MB | Accepted |
| image_5.1mb.png | 5.1 MB | Rejected with error |
| large.svg | > 5 MB | Accepted (SVG exempt) |
| large_document.pdf | > 5 MB | Accepted |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant widget | Composer visible with empty state |
| 2 | Attach image_5mb_exact.png (exactly 5 MB) via click-to-browse | File accepted; thumbnail appears. No error. |
| 3 | Remove the attachment | Thumbnail removed |
| 4 | Attempt to attach image_5.1mb.png (5.1 MB) via click-to-browse | Clear error: "Image size exceeds the 5 MB limit". File NOT attached (no thumbnail). |
| 5 | Attempt to attach image_5.1mb.png via drag-and-drop | Same error message. File not attached. |
| 6 | Attach large.svg (> 5 MB) via click-to-browse | SVG is accepted — thumbnail or filename appears. No error. |
| 7 | Remove the SVG attachment | Thumbnail removed |
| 8 | Attach large_document.pdf (> 5 MB) via click-to-browse | PDF accepted — filename appears. No error. |
| 9 | Type a message and send with the PDF attached | Message sent. Bot responds without error. |

## Expected Final State

Message sent. Bot responds without error.

## Pass/Fail Criteria

**Pass:**
- Image exactly at 5 MB is accepted
- Image > 5 MB is rejected with a clear error
- SVG > 5 MB is accepted (exempt)
- Non-image files > 5 MB are accepted

**Fail:**
- Image at 5 MB is rejected (limit should be inclusive)
- Image > 5 MB is silently accepted without error
- SVG > 5 MB is rejected (must be exempt)
- No error message appears for oversized image
