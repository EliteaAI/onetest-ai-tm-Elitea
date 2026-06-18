---
id: ELITEA-0576
title: "Support Assistant — 10-File Attachment Limit Is Enforced and Counter Updates Correctly"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0576: Support Assistant — 10-File Attachment Limit Is Enforced and Counter Updates Correctly

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify the Support Assistant enforces the 10-file maximum per message, that the attachment counter decrements with each file added, and that attempting to add an 11th file shows a clear error.

**Coverage:**
- Counter decrements from 10 to 0 as files are added
- Attempting to attach an 11th file via click: file browser is disabled or error shown
- Attempting to attach an 11th file via drag-and-drop: clear error banner displayed
- Existing 10 attachments are unaffected by the 11th file rejection

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin
- Browser: Chrome/Edge (latest)
- 11 unique small test files prepared: file1.png through file11.png, each < 1 MB

## Test Data

file1.png through file11.png (each < 1 MB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant widget. Check the attach counter tooltip. | Tooltip reads "Attach files (10 left)". |
| 2 | Attach files one by one: file1.png through file10.png (10 files total) using click-to-browse. After each, check the counter. | Counter decrements: after file1 → "9 left", after file2 → "8 left", ..., after file10 → "0 left". Paperclip appears disabled or shows 0. |
| 3 | Attempt to attach file11.png via click: click the paperclip icon. | Either the file browser does not open (button disabled), or a clear error message appears: "Maximum 10 files allowed". file11.png is NOT added. |
| 4 | Attempt to attach file11.png via drag-and-drop: drag file11.png and drop it onto the compose area. | A clear error toast/banner appears: "You have reached the maximum attachment limit of 10 files". Drop is rejected. |
| 5 | Verify all 10 original file thumbnails are still visible and unaffected. | All 10 thumbnails intact. No files were removed or corrupted. |
| 6 | Type a message and click Send. | Message with all 10 files is sent. Bot responds. |

## Expected Final State

Message with all 10 files is sent. Bot responds.

## Pass/Fail Criteria

**Pass:**
- Counter decrements correctly from 10 to 0
- 11th file is rejected via both click and drag-and-drop
- Clear, user-readable error message appears for the 11th file attempt
- Original 10 files remain intact after rejection

**Fail:**
- Counter does not decrement
- 11th file is silently accepted (limit not enforced)
- No error message shown for 11th file
- Existing attachments are corrupted or removed when 11th file is rejected
