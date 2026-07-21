---
id: ELITEA-2095
title: "Open Existing Conversation from Today Section"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:chat]
requirements: []
automation_test_id: tests.ui.chat.test_open_conversation_today_section.TestOpenConversationFromTodaySection.test_open_conversation_from_today_section
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/693
---

# ELITEA-2095: Open Existing Conversation from Today Section

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking a conversation from the Today section displays the full message history with scroll, an active input field, and the correct participant in the PARTICIPANTS panel.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Today section.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to the Private or Team project and go to Chats | Chats page is displayed |
| 2 | Locate the Today section in the middle panel and verify it is expanded with conversations listed | Today section visible with conversations |
| 3 | Click on a conversation from the Today list | Conversation content is displayed in the interaction window with full message history |
| 4 | Verify scroll functionality is available | Message history is scrollable |
| 5 | Verify the message input field at the bottom is active and ready for input | Input field is active |
| 6 | Verify the model or agent name is displayed in the input bar | Model/agent name visible |
| 7 | Verify the Context Budget indicator is shown in the bottom right with Messages and Summaries counters | Context Budget widget visible |
| 8 | Verify the PARTICIPANTS panel on the right shows the correct participant | PARTICIPANTS panel shows correct participant |

---

## Expected Final State

The conversation opens correctly with full message history, active input, context budget widget, and correct participant information.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Conversation opens with all expected UI elements visible.

**Fail:**
- Any step produces an error or unexpected result.
- Conversation does not load or expected UI elements are missing.
