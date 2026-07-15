---
id: ELITEA-2096
title: "Open Existing Conversation from This Week Section"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2096: Open Existing Conversation from This Week Section

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that the This Week section is collapsed by default and that expanding it and clicking a conversation displays the full message history with an active input field.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the This Week section.

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
| 2 | Locate the This Week section and verify it is collapsed by default | This Week shows only section label with arrow |
| 3 | Click the This Week section header to expand it | Conversations from the current week are listed |
| 4 | Click on a conversation from the This Week list | Conversation content is displayed with full message history and scroll |
| 5 | Verify the message input field is active and ready for input | Input field active |
| 6 | Verify the correct model or agent name is displayed in the input bar | Model/agent name visible |
| 7 | Verify the PARTICIPANTS panel reflects the correct participant | PARTICIPANTS shows correct participant |

---

## Expected Final State

The This Week section expands when clicked and conversations open correctly with full history and active input.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Section expands; conversation opens with history and active input.

**Fail:**
- Any step produces an error or unexpected result.
- Section does not expand or conversation does not load.
