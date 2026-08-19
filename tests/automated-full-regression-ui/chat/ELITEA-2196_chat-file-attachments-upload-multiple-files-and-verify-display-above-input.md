---
id: ELITEA-2196
title: "Chat – File Attachments – Upload Multiple Files and Verify They Display Above Message Input Field"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_attach_files_multiple_chips_display.TestAttachFilesMultipleChipsDisplay.test_attach_multiple_files_displays_chips_above_composer"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1595
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2196: Chat – File Attachments – Upload Multiple Files and Verify They Display Above Message Input Field

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that uploading multiple files shows them as chips above the message input field with filename and X button.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation and test files are available.

---

## Test Data

| Field | Value |
|-------|-------|
| Files to upload | 4-5 test files |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Click + icon, select 'Attach Files' | File picker opens |
| 2 | Select 4-5 files to upload | Files begin uploading |
| 3 | Verify files are displayed as chips above message input field | Chips visible in horizontal row |
| 4 | Verify each chip shows file icon and filename | Icon and name visible |
| 5 | Verify each chip has an X (close) button | X button on each chip |
| 6 | Verify chips have dark background with light text | Styling correct |

---

## Expected Final State

Uploaded files shown as chips above message input.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Files displayed as chips with icon, name, and X button.

**Fail:**
- Any step produces an error or unexpected result.
- Chips not shown or styling wrong.
