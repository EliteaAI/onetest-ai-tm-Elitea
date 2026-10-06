---
id: ELITEA-2467
title: "Chat – Attached files display with filenames, icons, and truncation for long names"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2467: Chat – Attached files display with filenames, icons, and truncation for long names

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that Chat – Attached files display with filenames, icons, and truncation for long names. Success is confirmed when verify the "+n" indicator is clickable to expand or scroll to view more files.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Chats section and attach files of different types (e.g. image, PDF, text) | Target page/section loads successfully. |
| 2 | Verify each chip shows a file icon on the left and filename next to it | Condition holds as described. |
| 3 | Verify long filenames are truncated with "..." to fit in the chip | Condition holds as described. |
| 4 | Verify chips have consistent dark background styling and are clearly readable | Condition holds as described. |
| 5 | Verify if more than 4-5 files are attached a "+N" indicator shows additional count | Condition holds as described. |
| 6 | Verify the "+N" indicator is clickable to expand or scroll to view more files | Condition holds as described. |

---

## Expected Final State

Verify the "+N" indicator is clickable to expand or scroll to view more files.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – Attached files display with filenames, icons, and truncation for long names.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
