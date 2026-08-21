---
id: ELITEA-2674
title: "Stop button does not break normal message sending in agents chat"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, issue:5000]
requirements: [EliteaAI/elitea_issues#5000]
---
# ELITEA-2674: Stop button does not break normal message sending in agents chat

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that implementing the new Stop button behavior does not prevent users from sending and receiving messages in agents chat when Stop is not clicked.

## Preconditions

- User is logged in to `{{base_url}}`
- At least one active agent is available
- Agents chat interface is accessible

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test Message 1 | "Test message for agent flow" |
| Test Message 2 | "Second test message" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to agents chat interface | Agents chat interface loads successfully |
| 2 | Select an active agent from the list | Agent is selected and chat interface is ready |
| 3 | Type "Test message for agent flow" in the input field | Text appears in the input field |
| 4 | Click Send button (do not click Stop) | Message appears in the chat thread as a user message |
| 5 | Wait for agent response to complete | Agent response is generated and displayed in the chat thread |
| 6 | Type "Second test message" in the input field | Text appears in the input field |
| 7 | Click Send button | Second message appears in the chat thread |
| 8 | Wait for agent response to complete | Second agent response is generated and displayed correctly |

## Expected Final State

Chat thread contains both user messages and their corresponding agent responses in the correct order. Input field is empty and ready for new input.

## Pass/Fail Criteria

**Pass:**
- Both messages successfully sent without clicking Stop
- Both agent responses generated completely
- Chat thread displays all messages and responses in correct order
- No errors or UI freezing occurs

**Fail:**
- Messages fail to send
- Agent responses are not generated
- Chat thread does not display messages correctly
- Any error messages appear
