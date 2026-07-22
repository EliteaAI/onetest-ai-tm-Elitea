---
id: ELITEA-2460
title: "Chat – Folder displays conversations when expanded and empty state when no conversations"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2460: Chat – Folder displays conversations when expanded and empty state when no conversations

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that Chat – Folder displays conversations when expanded and empty state when no conversations. Success is confirmed when verify the folder shows "no conversations added" text inside.

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
| 1 | Navigate to the Chats section and click a folder with conversations to expand it | Target page/section loads successfully. |
| 2 | Verify conversations are listed below the folder name when expanded | Condition holds as described. |
| 3 | Click the folder again to collapse it and verify conversations are hidden | Control responds; expected next state is shown. |
| 4 | Click an empty folder to expand it | Control responds; expected next state is shown. |
| 5 | Verify the folder shows "No conversations added" text inside | Condition holds as described. |

---

## Expected Final State

Verify the folder shows "No conversations added" text inside.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – Folder displays conversations when expanded and empty state when no conversations.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
