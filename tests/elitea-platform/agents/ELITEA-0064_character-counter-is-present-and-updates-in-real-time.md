---
id: ELITEA-0064
title: "Character Counter Is Present and Updates in Real Time"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
automation_test_id:
  - test_agent_character_limits.py:TestWelcomeMessageCharacterLimit.test_welcome_message_counter_visible_and_updates_realtime
  - test_agent_character_limits.py:TestWelcomeMessageCharacterLimit.test_welcome_message_fullscreen_counter_and_warning
  - test_agent_character_limits.py:TestConversationStarterCharacterLimit.test_conversation_starter_counter_visible_and_updates
  - test_agent_character_limits.py:TestConversationStarterCharacterLimit.test_conversation_starter_fullscreen_counter_and_warning
tags: [meta:reported-by-support, nfr:validation, nfr:usability, eng:frontend, feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4963]
---
# ELITEA-0064: Character Counter Is Present and Updates in Real Time

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that a live character counter is now visible in Inline (collapsed) mode and Full Screen mode for Welcome Message and Conversation Starter fields, and updates on each keystroke.

**Coverage:**
- Counter visible in Full Screen for both fields
- Real-time counter decrement on input
- Counter increment on deletion

## Preconditions

- Logged in to {{base_url}}
- Existing agent open in edit mode in the Private project

## Test Data

- Field 1: Welcome Message (Collapsed mode)
- Field 2: Conversation Starter (Collapsed mode)
- Field 3: Welcome Message (Full Screen editor)
- Field 4: Conversation Starter (Full Screen editor)
- Input string: 10 characters (e.g., "aaaaaaaaaa")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In the Welcome Message section in input field type 10 characters (e.g., 'xxxxxx'). | Counter appears with information how many characters left (format '758 characters left'). |
| 2 | Add 5 more characters. | Counter decreases by 5 in real time (format '763 characters left'). |
| 3 | Clear input field. | Counter disappears. |
| 4 | In the Welcome Message section of the left configuration panel, click the Full Screen/expand icon to open the Full Screen editor. | Full Screen editor opens with Welcome Message content. |
| 5 | Verify a character counter is visible in the Full Screen editor (format '768 characters left'). | Counter is present. |
| 6 | Type 10 characters (e.g., 'aaaaaaaaaa'). | Counter decreases by 10 in real time (format '758 characters left'). |
| 7 | Add 5 more characters. | Counter decreases by 5 in real time (format '763 characters left'). |
| 8 | Close the Full Screen editor. In the Conversation Starters section create new starter, type in input field 10 characters | Counter appears with information how many characters left (format '758 characters left'). |
| 9 | Repeat steps 2-3 for Conversation Starter |  |
| 10 | Open Full Screen mode for Conversation Starter. Verify a character counter is visible in this Full Screen editor. | Counter is present. |
| 11 | Type 10 characters. Then 5 more characters | Counter decreases by 10 and then by 5 in real time. |

## Expected Final State

Counter decreases by 10 and then by 5 in real time.

## Pass/Fail Criteria

**Pass:**
- Counter is visible in Full Screen mode for both Welcome Message and Conversation Starter
- Counter value updates immediately on each keystroke (increment on delete, decrement on type)

**Fail:**
- Counter is absent in Full Screen mode for either field
- Counter does not update in real time (remains static or updates only on save)
