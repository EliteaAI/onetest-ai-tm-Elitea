---
id: ELITEA-0575
title: "Support Assistant — Attached Files Display Correct Thumbnails or Filenames in Compose Area"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0575: Support Assistant — Attached Files Display Correct Thumbnails or Filenames in Compose Area

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify image files show visual thumbnail previews and document/data files show filename with icon in the compose area, and the counter updates correctly with multiple attachments.

**Coverage:**
- Image (PNG, JPG) shows visual thumbnail preview
- Document (PDF, DOCX) shows filename and icon (not blank/broken)
- Counter reflects attached files remaining (10 minus count attached)
- Compose area layout is intact with multiple attachments

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin
- Browser: Chrome/Edge (latest)

## Test Data

image.png (< 1 MB), photo.jpg (< 1 MB), sample.pdf (< 1 MB), report.docx (< 1 MB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Support Assistant widget. Confirm "Attach files (10 left)". | Empty composer. Counter at 10. |
| 2 | Attach image.png via click-to-browse | Visual thumbnail preview of image.png appears in compose area. Counter shows "9 left". |
| 3 | Attach photo.jpg via click-to-browse | Visual thumbnail preview of photo.jpg appears. Counter shows "8 left". |
| 4 | Attach sample.pdf via click-to-browse | File icon + filename "sample.pdf" appears (no broken or blank area). Counter shows "7 left". |
| 5 | Attach report.docx via click-to-browse | File icon + filename "report.docx" appears. Counter shows "6 left". |
| 6 | Observe the compose area with all 4 attachments | All 4 thumbnails/names visible. Layout intact — no overflow, no hidden or cut-off elements. Text input remains usable. |
| 7 | Type "Please process all attached files." alongside the attachments | Text input remains functional; text appears alongside attachment row. |
| 8 | Click Send | All 4 files sent with the message. Bot responds. |

## Expected Final State

All 4 files sent with the message. Bot responds.

## Pass/Fail Criteria

**Pass:**
- Image files show visual thumbnail previews
- Document files show filename with file icon (not blank)
- Counter decrements correctly with each attachment
- Compose area layout remains intact with multiple attachments

**Fail:**
- Image thumbnails show as blank, broken, or filename-only
- Document filenames are missing or blank
- Counter does not update
- Compose area overflows, hides the text input, or breaks layout
