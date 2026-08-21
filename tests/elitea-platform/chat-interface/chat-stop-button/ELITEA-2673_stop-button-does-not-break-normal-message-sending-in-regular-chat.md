---
id: ELITEA-2673
title: "Stop button does not break normal message sending in regular chat"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, issue:5000]
requirements: [EliteaAI/elitea_issues#5000]
---
# ELITEA-2673: Stop button does not break normal message sending in regular chat

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that implementing the new Stop button behavior does not prevent users from sending and receiving messages in regular chat when Stop is not clicked.

## Preconditions

- User is logged in to `{{base_url}}`
- Regular chat interface is accessible

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test Message 1 | "Test message for normal flow" |
| Test Message 2 | "Second test message" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open regular chat interface | Chat interface loads successfully with message input field visible |
| 2 | Type "Test message for normal flow" in the input field | Text appears in the input field |
| 3 | Click Send button (do not click Stop) | Message appears in the chat thread as a user message |
| 4 | Wait for AI response to complete | AI response is generated and displayed in the chat thread |
| 5 | Type "Second test message" in the input field | Text appears in the input field |
| 6 | Click Send button | Second message appears in the chat thread |
| 7 | Wait for AI response to complete | Second AI response is generated and displayed correctly |

## Expected Final State

Chat thread contains both user messages and their corresponding AI responses in the correct order. Input field is empty and ready for new input.

## Pass/Fail Criteria

**Pass:**
- Both messages successfully sent without clicking Stop
- Both AI responses generated completely
- Chat thread displays all messages and responses in correct order
- No errors or UI freezing occurs

**Fail:**
- Messages fail to send
- AI responses are not generated
- Chat thread does not display messages correctly
- Any error messages appear
