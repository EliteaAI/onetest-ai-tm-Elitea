---
id: ELITEA-0059
title: "Counter Turns Red When Character Count Reaches Zero in Full Screen Mode"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.agents.test_agent_character_limits.TestWelcomeMessageCharacterCounter.test_welcome_message_fullscreen_counter_and_warning
  - tests.ui.agents.test_agent_character_limits.TestConversationStarterCharacterCounter.test_conversation_starter_fullscreen_counter_and_warning
tags: [meta:reported-by-support, nfr:validation, nfr:usability, eng:frontend, feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4963]
---
# ELITEA-0059: Counter Turns Red When Character Count Reaches Zero in Full Screen Mode

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the character counter changes to red and the warning message appears when the 768-character limit is reached in Full Screen editor mode for Welcome Message and Conversation Starter fields.

**Coverage:**
- Counter color turns red at BV1 (768 chars)
- Warning message "0 characters left. You have reached the MAXIMUM character limit" shown at BV1
- Input blocked or truncated at BV2 (769 chars); counter remains red
- Counter reverts to default color above 0

## Preconditions

- Logged in to {{base_url}}
- Existing agent open in edit mode
- Full Screen editor open for the Welcome Message field

## Test Data

- BV1: 768-character string — exactly at the character limit (counter = 0)
- BV2: 769-character string — one over the character limit (input blocked or truncated)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Full Screen editor for the Welcome Message field. Note the default counter color. | Counter is visible in a neutral/default color (not red). |
| 2 | Clear the field. Paste the BV1 string (768 chars). | Counter shows 0. Counter text color changes to red. Warning message '0 characters left. You have reached the MAXIMUM character limit' is displayed. |
| 3 | Delete 1 character. | Counter shows 1. Counter color reverts to default (non-red). Warning message disappears. |
| 4 | Type 2 characters to return to the limit (BV2 — 769 chars attempted). | Input is blocked or truncated at 768 chars. Counter shows 0. Counter remains red. Warning message '0 characters left. You have reached the MAXIMUM character limit' is shown. |
| 5 | Close the Full Screen editor. Open a Conversation Starter entry's Full Screen editor. Repeat steps 1–4 for this field. | Same counter color and warning message behavior observed for the Conversation Starter field. |

## Expected Final State

Same counter color and warning message behavior observed for the Conversation Starter field.

## Pass/Fail Criteria

**Pass:**
- Counter turns red at exactly 0 (BV1 = 768 chars) for both fields in Full Screen mode
- Warning "0 characters left. You have reached the MAXIMUM character limit" appears at 0
- Counter and warning revert to default when count rises above 0

**Fail:**
- Counter does not change color at 0 for either field
- Warning message does not appear or shows different text
- Counter turns red before 0 or stays red above 0
