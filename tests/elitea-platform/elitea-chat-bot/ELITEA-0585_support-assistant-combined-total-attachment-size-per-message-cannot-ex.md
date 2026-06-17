---
id: ELITEA-0585
title: "Support Assistant — Combined Total Attachment Size Per Message Cannot Exceed 150 MB"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0585: Support Assistant — Combined Total Attachment Size Per Message Cannot Exceed 150 MB

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that when the combined size of all attached files exceeds 150 MB, the user receives a clear error and the message is not sent silently.

**Coverage:**
- Attachments with combined size under 150 MB: accepted and sent
- Adding a file that pushes total above 150 MB: rejected with clear error
- First valid attachment remains intact after rejection of second
- User can remove attachments and retry

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin
- Browser: Chrome/Edge (latest)
- Test files: large_file_1.pdf (80 MB), large_file_2.pdf (80 MB). Combined = 160 MB > 150 MB limit.

## Test Data

- large_file_1.pdf (80 MB)
- large_file_2.pdf (80 MB)
- Combined total = 160 MB (exceeds 150 MB limit)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant widget | Composer visible |
| 2 | Attach large_file_1.pdf (80 MB) via click-to-browse | File attached. No error (80 MB < 150 MB limit). Filename visible in compose area. |
| 3 | Attempt to attach large_file_2.pdf (80 MB) — combined would be 160 MB | Clear error message: "Total attachment size exceeds 150 MB". large_file_2.pdf is NOT added. |
| 4 | Confirm large_file_1.pdf thumbnail is still present in compose area | large_file_1.pdf intact and unaffected. |
| 5 | Type a message and send with only large_file_1.pdf (80 MB) | Message sent successfully. Bot responds. |
| 6 | Start a new message. Attach only large_file_1.pdf then remove it. Confirm user can retry with files within the limit. | No error for within-limit attachment. Removal works correctly. |

## Expected Final State

No error for within-limit attachment. Removal works correctly.

## Pass/Fail Criteria

**Pass:**
- Files within 150 MB combined are accepted
- Adding a file that pushes total above 150 MB is rejected with a clear error
- First valid attachment remains intact after rejection
- User can retry with corrected file combination

**Fail:**
- Files totaling > 150 MB are silently accepted
- Error message is missing or unclear
- First valid attachment is removed when second is rejected
- Send is blocked even for attachments under 150 MB
