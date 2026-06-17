---
id: ELITEA-0507
title: "SVG files are exempt from the 5 MB image size limit and are not counted toward the 10-file attachment limit"
priority: medium
type: functional
module: chat-attachments
status: ready
execution_type: manual
tags: [feat:attachments, issue:1285, feat:chat, r-2.0.0b]
requirements: [ProjectAlita/projectalita.github.io#1285]
---
# ELITEA-0507: SVG files are exempt from the 5 MB image size limit and are not counted toward the 10-file attachment limit

**Module:** Chat Attachments · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the two documented SVG exemptions: (1) SVG files larger than 5 MB are accepted without triggering the image size limit error, and (2) SVG files do not count toward the maximum 10 non-SVG images per message limit.

**Coverage:**
- SVG file > 5 MB accepted — not rejected by the image size limit
- SVG files excluded from the 10-file non-SVG image count
- After 10 non-SVG images attached, an additional SVG is still accepted
- Attempting an 11th non-SVG image is blocked (confirming SVG exemption is real, not a general limit bypass)

## Preconditions

- Logged into ELITEA at {{base_url}}
- `large_vector.svg` file > 5 MB available locally
- 10 × `.jpg` images (each < 5 MB) with distinct filenames
- 1 additional `extra.svg` file

## Test Data

- `large_vector.svg`: SVG file exceeding 5 MB
- `image_01.jpg` through `image_10.jpg`: 10 distinct JPG files under 5 MB each
- `extra.svg`: any small SVG file

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation → click the paperclip → select `large_vector.svg` (> 5 MB) | SVG file accepted without any '5 MB image limit' error; thumbnail appears in the input area |
| 2 | Clear the input. Attach `image_01.jpg` through `image_10.jpg` one by one (10 JPG images total) | All 10 JPG thumbnails appear in the input; no error shown after the 10th |
| 3 | With 10 JPGs already attached, attach `extra.svg` | `extra.svg` is accepted as an additional attachment; no error — SVG is not counted toward the 10-image non-SVG limit; 11 thumbnails visible total |
| 4 | With the same 10 JPGs still attached, attempt to attach an 11th JPG file | 11th JPG is rejected with a toast warning (e.g., 'Maximum 10 image attachments allowed'); only 10 JPGs remain in the input (confirming the limit applies to non-SVG images only) |

## Expected Final State

11th JPG is rejected with a toast warning (e.g., 'Maximum 10 image attachments allowed'); only 10 JPGs remain in the input (confirming the limit applies to non-SVG images only)

## Pass/Fail Criteria

**Pass:**
- SVG > 5 MB accepted without size error
- SVG does not count toward the 10-image cap; 10 JPGs + extra.svg all accepted
- 11th JPG correctly rejected with toast warning

**Fail:**
- SVG > 5 MB rejected for size
- SVG counted toward 10-file limit causing premature rejection
- 11th JPG accepted silently (limit not enforced)
