---
id: ELITEA-0579
title: "Support Assistant — Attached Files Can Be Removed Individually from Compose Area Before Sending"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0579: Support Assistant — Attached Files Can Be Removed Individually from Compose Area Before Sending

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify the user can remove individual attached files from the compose area before sending, the counter increments back, and only the remaining files are sent.

**Coverage:**
- Remove (X) button appears on hover over attachment thumbnail
- Clicking Remove removes only that specific file
- Counter increments correctly after removal
- Remaining files are unaffected
- Only non-removed files are sent with the message

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin
- Browser: Chrome/Edge (latest)

## Test Data

file_a.png (< 1 MB), file_b.jpg (< 1 MB), file_c.pdf (< 1 MB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant widget | Empty composer |
| 2 | Attach file_a.png, file_b.jpg, and file_c.pdf via click-to-browse | All 3 thumbnails visible in compose area. Counter shows "7 left". |
| 3 | Hover over the file_b.jpg thumbnail | A Remove (X) button or control becomes visible on the thumbnail |
| 4 | Click the Remove/X button for file_b.jpg | file_b.jpg thumbnail removed. Counter increments to "8 left". file_a.png and file_c.pdf remain visible and unaffected. |
| 5 | Hover over file_a.png thumbnail and click its Remove button | file_a.png removed. Counter shows "9 left". file_c.pdf remains. |
| 6 | Type "Please process the attached PDF." | Text appears in composer |
| 7 | Click Send | Message sent with only file_c.pdf attached. file_a.png and file_b.jpg are NOT included. Bot responds acknowledging the PDF. |

## Expected Final State

Message sent with only file_c.pdf attached. file_a.png and file_b.jpg are NOT included. Bot responds acknowledging the PDF.

## Pass/Fail Criteria

**Pass:**
- Remove (X) control appears on hover over each thumbnail
- Clicking Remove removes only that specific file
- Counter increments correctly after each removal
- Other attachments are unaffected
- Only remaining files are sent

**Fail:**
- No Remove/X control appears on thumbnail
- Removing one file removes all attachments
- Counter does not increment after removal
- Removed files still appear to be sent (bot references them)
