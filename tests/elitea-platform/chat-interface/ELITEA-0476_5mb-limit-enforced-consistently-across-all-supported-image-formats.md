---
id: ELITEA-0476
title: "5MB Limit Enforced Consistently Across All Supported Image Formats"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:attachments, file-validation, image-upload, chat]
requirements: [ProjectAlita/projectalita.github.io#3624]
---
# ELITEA-0476: 5MB Limit Enforced Consistently Across All Supported Image Formats

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the 5MB upload limit is enforced uniformly for every image MIME type supported by the platform (.jpg, .jpeg, .png, .gif, .webp) — no image format silently bypasses the restriction.

## Preconditions

- Logged in to {{base_url}} with a valid user account
- A Chat conversation with file/image attachment enabled is open
- One oversized (~8MB) test image file prepared for each format below

## Test Data

| File | Format | Size |
|------|--------|---------|
| oversize_test.jpg  | .jpg  | ~8MB |
| oversize_test.jpeg | .jpeg | ~8MB |
| oversize_test.png  | .png  | ~8MB |
| oversize_test.gif  | .gif  | ~8MB |
| oversize_test.webp | .webp | ~8MB |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation with attachment support. | Attachment button is enabled. |
| 2 | Click the attachment button and select oversize_test.jpg (~8MB). | File is rejected immediately. A 5MB limit error message appears. The file does not appear in the attachment preview. |
| 3 | Repeat step 2 for oversize_test.jpeg (~8MB). | File is rejected with the 5MB error. |
| 4 | Repeat step 2 for oversize_test.png (~8MB). | File is rejected with the 5MB error. |
| 5 | Repeat step 2 for oversize_test.gif (~8MB). | File is rejected with the 5MB error. |
| 6 | Repeat step 2 for oversize_test.webp (~8MB). | File is rejected with the 5MB error. |
| 7 | Confirm that the error message appeared for all 5 formats and that no format was accepted silently or with a different error. | 5MB rejection error appears for all 5 formats. No format bypasses the limit. |

## Expected Final State

5MB rejection error appears for all 5 formats. No format bypasses the limit.

## Pass/Fail Criteria

Pass:
- All 5 image formats trigger the 5MB rejection error when the file exceeds 5MB
- No format accepts an oversized image silently
- No format produces a different/unrelated error

Fail:
- Any image format accepts the oversized file without error
- Any image format produces an unexpected error (e.g., "invalid type") instead of the 5MB limit message
- The restriction is only applied to a subset of image formats (e.g., only .jpg)
