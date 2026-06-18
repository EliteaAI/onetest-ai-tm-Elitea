---
id: ELITEA-0572
title: "Support Assistant — Validation Error Clears and Send Button Re-enables After Reducing Attachments Below 10-File Limit"
priority: critical
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#5017, EliteaAI/elitea_issues#4777]
---
# ELITEA-0572: Support Assistant — Validation Error Clears and Send Button Re-enables After Reducing Attachments Below 10-File Limit

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a user attaches more than 10 files (triggering the "Max 10 attachments allowed" error state) and then removes files to bring the count to 10 or fewer, the red highlighting is automatically removed, the validation error clears, and the Send button becomes enabled.

**Bug Reference:** EliteaAI/elitea_issues#5017 — File attachment validation state persists after reducing attachments below the 10-file limit.

**Coverage:**
- Attaching 11+ files triggers "Max 10 attachments allowed" warning and red highlighting on attachment chips
- Removing files until ≤10 remain clears the red highlighting automatically
- Validation error message disappears when count drops to ≤10
- Send button becomes enabled once the count is valid (≤10 files + text input non-empty)
- Regression: confirming the error state does NOT persist as a false positive

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin (Admin → Guardrails → toggle ON)
- Browser: Chrome/Edge (latest)
- 12 unique small test files prepared locally (e.g., file01.png through file12.png, each < 1 MB)

## Test Data

file01.png through file12.png — each < 1 MB, unique names
(Attach 10 → then attempt 11th → remove to return to ≤10)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant widget by clicking the floating launcher in the bottom-right corner | Widget opens with an empty composer. Attach counter tooltip reads "Attach files (10 left)". |
| 2 | Type "Please review all attached files." in the text input | Text appears in the composer. Send button is still disabled (no files attached yet). |
| 3 | Click the paperclip icon and select file01.png through file10.png (10 files at once) from the file browser | All 10 files are attached. Thumbnails/filenames appear in the compose area. Counter shows "0 left". No error shown. Send button is enabled. |
| 4 | Click the paperclip again and attempt to attach file11.png | file11.png is rejected OR drag/drop triggers "Max 10 attachments allowed" warning. Attachment chips for the original 10 files are highlighted in red. Send button becomes disabled. |
| 5 | Alternatively, drag file11.png and drop it onto the compose area to trigger the error state if step 4 did not produce it | "Max 10 attachments allowed" warning is visible. All attachment chips are highlighted in red. Send button is disabled. |
| 6 | Remove file11.png by clicking its X button (so total count returns to 10) | file11.png is removed. Total count is now 10 (≤ limit). Red highlighting is automatically removed from all remaining chips. "Max 10 attachments allowed" warning disappears. Send button becomes enabled. |
| 7 | Click Send | Message with 10 files is sent successfully. Bot responds. No error occurs. |
| 8 | Start a new message. Attach 11 files (file01.png–file11.png) to trigger the error again. Then remove 2 files (bringing total to 9). | After removing 2 files (total = 9): red highlighting clears, warning disappears, Send button is enabled. |
| 9 | Click Send on the message with 9 files | Message sent successfully. Bot responds. |

## Expected Final State

Message sent successfully. Bot responds.

## Pass/Fail Criteria

**Pass:**
- Red highlighting and "Max 10 attachments allowed" warning appear when 11+ files are attached
- Both the red highlights AND the warning message clear automatically when count is reduced to ≤10
- Send button becomes enabled once count is valid and text is present
- Message sends successfully with ≤10 files after the error state clears

**Fail (bug reproduced — EliteaAI/elitea_issues#5017):**
- Red highlighting persists on attachment chips even after reducing count to ≤10
- "Max 10 attachments allowed" message remains visible even with ≤10 files
- Send button remains disabled even after reducing to a valid file count
- User is unable to send the message despite having a valid number of attachments
