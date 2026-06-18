---
id: ELITEA-0504
title: "Maximum 10 non-SVG files per message enforced — 11th non-SVG attachment shows a toast warning"
priority: medium
type: functional
module: chat-attachments
status: ready
execution_type: manual
tags: [feat:attachments, issue:1285, feat:chat, r-2.0.0b]
requirements: [ProjectAlita/projectalita.github.io#1285]
---
# ELITEA-0504: Maximum 10 non-SVG files per message enforced — 11th non-SVG attachment shows a toast warning

**Module:** Chat Attachments · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that attaching more than 10 non-SVG image files to a single message is blocked with a visible toast warning — the 11th file is not accepted, silently dropped, or added without notification.

**Coverage:**
- Up to 10 non-SVG attachments accepted per message without error
- 11th non-SVG file triggers a descriptive toast warning (e.g., "Maximum N image attachments allowed")
- 11th file does NOT appear as a thumbnail in the input
- Exactly 10 thumbnails remain visible after the rejection
- Limit applies independently of total message size

## Preconditions

- Logged into ELITEA at {{base_url}}
- 11 × `.jpg` images available locally, all distinct filenames, each under 5 MB

## Test Data

- Files: `img_01.jpg` through `img_11.jpg` (11 distinct JPG files, each < 5 MB)
- Total combined size of 11 files: well under 150 MB

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation → click the paperclip → attach `img_01.jpg` through `img_10.jpg` one by one | All 10 thumbnails appear in the input; no error or restriction shown after the 10th image |
| 2 | Count the thumbnails in the input area | Exactly 10 image thumbnails are visible |
| 3 | Click the paperclip again → attempt to attach `img_11.jpg` | A toast notification appears: "Maximum N image attachments allowed" (or equivalent wording indicating the limit is reached); `img_11.jpg` is NOT added to the input |
| 4 | Count the thumbnails again | Still exactly 10 thumbnails — the 11th file was rejected and is not present |

## Expected Final State

Still exactly 10 thumbnails — the 11th file was rejected and is not present

## Pass/Fail Criteria

**Pass:**
- 10 non-SVG images accepted; 11th triggers a descriptive toast warning
- 11th file not added to the input
- Thumbnail count remains at 10 after rejection attempt

**Fail:**
- 11th file silently dropped with no notification
- All 11 files accepted without enforcement
- Toast message is generic or absent
- Thumbnail count shows 11
