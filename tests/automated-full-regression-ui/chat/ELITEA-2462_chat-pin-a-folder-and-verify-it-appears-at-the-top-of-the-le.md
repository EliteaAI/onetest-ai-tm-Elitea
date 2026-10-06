---
id: ELITEA-2462
title: "Chat – Pin a folder and verify it appears at the top of the left panel"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2462: Chat – Pin a folder and verify it appears at the top of the left panel

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that Chat – Pin a folder and verify it appears at the top of the left panel. Success is confirmed when verify the folder is no longer present in its original unpinned position.

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
| 1 | Navigate to the Chats section and identify an unpinned folder | Target page/section loads successfully. |
| 2 | Hover over the folder, click the three-dot icon, and click Pin on top | Action completes without error and produces the expected UI state. |
| 3 | Verify the folder moves to the top of the left panel in the pinned folders section | Condition holds as described. |
| 4 | Verify a pin icon is displayed next to the folder name | Condition holds as described. |
| 5 | Verify the folder still displays all its conversations when expanded | Condition holds as described. |
| 6 | Verify the folder is no longer present in its original unpinned position | Condition holds as described. |

---

## Expected Final State

Verify the folder is no longer present in its original unpinned position.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – Pin a folder and verify it appears at the top of the left panel.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
