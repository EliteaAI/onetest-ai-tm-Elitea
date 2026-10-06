---
id: ELITEA-2459
title: "Chat – Folder rename – validation tooltip for invalid input and first character cannot be a space"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2459: Chat – Folder rename – validation tooltip for invalid input and first character cannot be a space

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that Chat – Folder rename – validation tooltip for invalid input and first character cannot be a space. Success is confirmed when verify the space is not accepted as the first character and the checkmark remains inactive.

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
| 2 | Clear the current name and type a name with unsupported special characters (e.g. "Folder$$%%") | Action completes without error and produces the expected UI state. |
| 3 | Verify a tooltip appears with the validation message: "The folder name should be 3 to 64 characters long. It can include letters (a-z, A-Z), numbers (0-9), underscores (_), brackets ([]), parentheses (()), dots (.), hyphen(-), and spaces. Please note that the first character should not be a space." | Condition holds as described. |
| 4 | Verify the checkmark icon is disabled and clicking it has no effect | Condition holds as described. |
| 5 | Clear the name and press the Space key as the first character | Action completes without error and produces the expected UI state. |
| 6 | Verify the space is not accepted as the first character and the checkmark remains inactive | Condition holds as described. |

---

## Expected Final State

Verify the space is not accepted as the first character and the checkmark remains inactive.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – Folder rename – validation tooltip for invalid input and first character cannot be a space.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
