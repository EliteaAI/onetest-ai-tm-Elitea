---
id: ELITEA-2097
title: "Open Existing Conversation from Older Section"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2097: Open Existing Conversation from Older Section

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Older section is collapsed by default and that expanding it and clicking a conversation displays the full message history with an active input field.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Older section.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to the Chats page | Chats page is displayed |
| 2 | Locate the Older section and verify it is collapsed by default | Older section shows only label with arrow |
| 3 | Click the Older section header to expand it | Conversations older than current week are listed |
| 4 | Click on a conversation from the Older list | Conversation content is displayed with full message history and scroll |
| 5 | Verify the message input field is active and ready for input | Input field active |
| 6 | Verify the correct model or agent name is displayed in the input bar | Model/agent name visible |
| 7 | Verify the PARTICIPANTS panel reflects the correct participant | PARTICIPANTS shows correct participant |

---

## Expected Final State

The Older section expands when clicked and conversations open correctly with full history and active input.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Section expands; conversation opens with history and active input.

**Fail:**
- Any step produces an error or unexpected result.
- Section does not expand or conversation does not load.
