---
id: ELITEA-0581
title: "Support Assistant — Attached Files in Compose Area Are Preserved When Switching Between Compact and Full View"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0581: Support Assistant — Attached Files in Compose Area Are Preserved When Switching Between Compact and Full View

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that files attached before sending are not lost when the user toggles between compact widget mode and full view mode.

**Coverage:**
- Attachments added in compact mode persist after expanding to full view
- Attachments added in compact mode persist after collapsing back from full view
- Counter accurately reflects attached files in both modes
- Sending from full view after attaching in compact works correctly

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin
- Browser: Chrome/Edge (latest)

## Test Data

file_a.png (< 1 MB), file_b.pdf (< 1 MB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant widget in compact mode | Widget open in compact mode |
| 2 | Attach file_a.png and file_b.pdf using the paperclip icon | Both thumbnails visible in compose area. Counter shows "8 left". |
| 3 | Click the expand icon to switch to full view mode | Widget expands to full view. Both file_a.png and file_b.pdf thumbnails are still visible. Counter still shows "8 left". |
| 4 | Observe the state — do not add any new files | Attachments preserved exactly as added in compact mode |
| 5 | Click the collapse icon to return to compact mode | Widget returns to compact. Both thumbnails still visible. Counter still shows "8 left". |
| 6 | Type "Please process both files." in the text input | Text appears alongside the attachment thumbnails |
| 7 | Click Send | Message with both files sent. Bot responds. |

## Expected Final State

Message with both files sent. Bot responds.

## Pass/Fail Criteria

**Pass:**
- Both attachments persist after expanding to full view
- Both attachments persist after collapsing back to compact
- Counter accurately reflects files in both modes
- All attached files are sent with the message

**Fail:**
- Any attachment is lost when switching to full view
- Any attachment is lost when switching back to compact
- Counter resets to 10 after mode toggle
- Sent message contains fewer files than were attached
