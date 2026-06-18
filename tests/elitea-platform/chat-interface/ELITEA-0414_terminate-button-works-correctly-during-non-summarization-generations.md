---
id: ELITEA-0414
title: "Terminate Button Works Correctly During Non-Summarization Generations — Regression"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:context-management, feat:chat, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3984]
---
# ELITEA-0414: Terminate Button Works Correctly During Non-Summarization Generations — Regression

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that after the fix for issue EliteaAI/elitea_issues#3984, the Terminate button still correctly interrupts active LLM generation when clicked — confirming the fix did not break the cancellation functionality.

**Coverage:**
- Terminate button is still displayed during active LLM generation (no regression on appearance)
- Clicking Terminate successfully cancels generation before completion
- Send button is restored after successful cancellation
- Conversation remains functional after an interrupted generation

## Preconditions

- Logged in to {{base_url}} with Editor/Admin role
- A Chat conversation is active (Context Budget may or may not be enabled)
- Browser: Chrome (latest)

## Test Data

- Generation-triggering message: "Write a detailed 2000-word essay on the complete history of personal computing from 1970 to the present"
- Post-termination message: "Continue from where you left off"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat → Conversations and open or create a conversation. | Chat input is accessible. |
| 2 | Send the message: 'Write a detailed 2000-word essay on the complete history of personal computing from 1970 to the present'. | LLM starts generating; Terminate button is displayed in the chat input area. |
| 3 | While the LLM is actively generating (response not yet complete), click the Terminate button. | Generation stops; partial response is left in the conversation. |
| 4 | Observe the chat input area immediately after clicking Terminate. | Send button is displayed (restored from Terminate). |
| 5 | Confirm the partial response in the conversation is not empty. | At least some generated content is visible. |
| 6 | Type 'Continue from where you left off' and click Send. | Message is submitted using the Send button. |
| 7 | Confirm the LLM generates a response and the button cycles: Send → Terminate → Send again. | Full button cycle completes without issues. |

## Expected Final State

Full button cycle completes without issues.

## Pass/Fail Criteria

**Pass:**
- Terminate button appears during active generation (no regression)
- Clicking Terminate stops generation immediately
- Send button is restored after cancellation
- Conversation is functional after an interrupted generation

**Fail:**
- Terminate button does not appear during generation
- Clicking Terminate does not stop generation
- Send button is not restored after cancellation
- Conversation becomes unresponsive after using Terminate
