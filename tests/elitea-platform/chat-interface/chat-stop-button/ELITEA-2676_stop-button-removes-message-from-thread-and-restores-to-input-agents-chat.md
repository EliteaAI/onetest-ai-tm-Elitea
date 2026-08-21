---
id: ELITEA-2676
title: "Stop button removes message from thread and restores it to input field in agents chat"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, issue:5000]
requirements: [EliteaAI/elitea_issues#5000]
---
# ELITEA-2676: Stop button removes message from thread and restores it to input field in agents chat

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking Stop during message processing in agents chat removes the user message from thread and restores it to the input field for editing.

## Preconditions

- User is logged in to `{{base_url}}`
- At least one active agent is available
- Agents chat interface is accessible

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test Message | "This is a test message for agent chat" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to agents chat interface | Agents chat interface loads successfully |
| 2 | Select an active agent from the list | Agent is selected and chat interface is ready |
| 3 | Type "This is a test message for agent chat" in the input field | Text appears in the input field |
| 4 | Click Send button | Message appears in the chat thread; agent response starts processing |
| 5 | Immediately click Stop button before agent response completes | Stop button is clicked successfully |
| 6 | Check the chat thread | User message "This is a test message for agent chat" is removed from the chat thread |
| 7 | Check the input field | Original text "This is a test message for agent chat" appears in the input field |
| 8 | Click in the input field and attempt to edit the text | Input field is editable; cursor responds to clicks and keyboard input |
| 9 | Check the chat thread for any agent response | Partial agent response (if any) is removed from the thread |

## Expected Final State

Chat thread does not contain the stopped user message or any partial agent response. Input field contains the original message text and is fully editable.

## Pass/Fail Criteria

**Pass:**
- User message is removed from the chat thread
- Original text is restored to the input field exactly as typed
- Input field is editable
- Partial agent response is removed from the thread
- No error messages or UI glitches occur

**Fail:**
- User message remains in the chat thread
- Text is not restored to the input field
- Input field is not editable
- Partial agent response remains visible
- Any error messages appear
