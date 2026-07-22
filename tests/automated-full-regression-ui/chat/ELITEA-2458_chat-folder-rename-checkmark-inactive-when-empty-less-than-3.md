---
id: ELITEA-2458
title: "Chat – Folder rename – checkmark inactive when empty, less than 3 characters, or no changes made"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2458: Chat – Folder rename – checkmark inactive when empty, less than 3 characters, or no changes made

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that Chat – Folder rename – checkmark inactive when empty, less than 3 characters, or no changes made. Success is confirmed when click the checkmark icon and verify the folder is renamed to "abc".

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
| 1 | Navigate to the Chats section, hover over any folder, click the three-dot icon and click Edit | Target page/section loads successfully. |
| 2 | Clear the entire content of the input field so it is empty | Action completes without error and produces the expected UI state. |
| 3 | Verify the checkmark icon is in a disabled/inactive state and clicking it has no effect | Condition holds as described. |
| 4 | Type exactly 2 characters (e.g. "AB") and verify the checkmark icon remains inactive | Field accepts the input and displays the entered value. |
| 5 | Verify the tooltip validation message is shown | Condition holds as described. |
| 6 | Do not change the pre-filled name and verify the checkmark is inactive with no effect when clicked | Action completes without error and produces the expected UI state. |
| 7 | Type one more character (total 3 characters e.g. "ABC") | Field accepts the input and displays the entered value. |
| 8 | Verify the checkmark icon becomes active/enabled | Condition holds as described. |
| 9 | Click the checkmark icon and verify the folder is renamed to "ABC" | Control responds; expected next state is shown. |

---

## Expected Final State

Click the checkmark icon and verify the folder is renamed to "ABC".

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – Folder rename – checkmark inactive when empty, less than 3 characters, or no changes made.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
