---
id: ELITEA-2675
title: "Stop button removes message from thread and restores it to input field in regular chat"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, issue:5000]
requirements: [EliteaAI/elitea_issues#5000]
---
# ELITEA-2675: Stop button removes message from thread and restores it to input field in regular chat

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking Stop during message processing in regular chat removes the user message from thread and restores it to the input field for editing.

## Preconditions

- User is logged in to `{{base_url}}`
- Regular chat interface is accessible

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test Message | "This is a test message that should be restored" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open regular chat interface | Chat interface loads successfully with message input field visible |
| 2 | Type "This is a test message that should be restored" in the input field | Text appears in the input field |
| 3 | Click Send button | Message appears in the chat thread; AI response starts processing |
| 4 | Immediately click Stop button before AI response completes | Stop button is clicked successfully |
| 5 | Check the chat thread | User message "This is a test message that should be restored" is removed from the chat thread |
| 6 | Check the input field | Original text "This is a test message that should be restored" appears in the input field |
| 7 | Click in the input field and attempt to edit the text | Input field is editable; cursor responds to clicks and keyboard input |
| 8 | Check the chat thread for any AI response | Partial AI response (if any) is removed from the thread |

## Expected Final State

Chat thread does not contain the stopped user message or any partial AI response. Input field contains the original message text and is fully editable.

## Pass/Fail Criteria

**Pass:**
- User message is removed from the chat thread
- Original text is restored to the input field exactly as typed
- Input field is editable
- Partial AI response is removed from the thread
- No error messages or UI glitches occur

**Fail:**
- User message remains in the chat thread
- Text is not restored to the input field
- Input field is not editable
- Partial AI response remains visible
- Any error messages appear
