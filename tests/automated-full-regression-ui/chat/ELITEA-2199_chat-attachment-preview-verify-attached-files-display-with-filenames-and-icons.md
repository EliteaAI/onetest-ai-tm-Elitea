---
id: ELITEA-2199
title: "Chat – Attachment Preview – Verify Attached Files Display with Filenames and Icons"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_attach_files_multiple_chips_display.TestAttachFilesMultipleChipsDisplay.test_attach_files_of_different_types_shows_identical_icon_and_long_filename_truncates"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1595
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2199: Chat – Attachment Preview – Verify Attached Files Display with Filenames and Icons

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that attached files show correct icons for their type and truncated filenames.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation and test files of different types are available.

---

## Test Data

| Field | Value |
|-------|-------|
| File types | image, PDF, text, etc. |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Click + icon, Attach Files; select files of different types | Files upload |
| 2 | Verify each file chip shows a type-appropriate icon on the left | Icons reflect file types |
| 3 | Verify filenames are shown next to icons | Filenames visible |
| 4 | Verify long filenames are truncated with '...' | Truncation applied |
| 5 | Verify chips have consistent dark background styling | Styling consistent |
| 6 | Verify if more than 4-5 files, a '+N' indicator shows additional count | +N indicator shown |

---

## Expected Final State

File chips display with correct icons and truncated filenames.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Icons and names shown correctly; truncation and +N work.

**Fail:**
- Any step produces an error or unexpected result.
- Icons or names missing or incorrect.
