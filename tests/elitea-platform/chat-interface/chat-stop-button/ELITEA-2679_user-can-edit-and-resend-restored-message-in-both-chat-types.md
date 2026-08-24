---
id: ELITEA-2679
title: "User can edit and successfully resend restored message in both chat types"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, issue:5000]
requirements: [EliteaAI/elitea_issues#5000]
---
# ELITEA-2679: User can edit and successfully resend restored message in both chat types

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that after Stop is clicked and the message is restored to the input field, the user can edit the text and successfully resend it in both regular chat and agents chat.

## Preconditions

- User is logged in to `{{base_url}}`
- Regular chat and agents chat interfaces are accessible
- At least one active agent is available for agents chat testing

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Original Message | "Original message text" |
| Edited Message | "Edited message text" |

## Steps

### Part 1: Regular Chat

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open regular chat interface | Chat interface loads successfully |
| 2 | Type "Original message text" in the input field | Text appears in the input field |
| 3 | Click Send button | Message is sent and appears in the chat thread |
| 4 | Click Stop button during AI response processing | Stop button is clicked; message is removed from thread |
| 5 | Verify "Original message text" appears in the input field | Message is restored to the input field |
| 6 | Edit the message in the input field to read "Edited message text" | Text is successfully edited; input field responds to keyboard input |
| 7 | Click Send button to resend the edited message | Edited message "Edited message text" appears in the chat thread |
| 8 | Wait for AI response to complete | AI response is generated for the edited message |
| 9 | Verify the AI response is relevant to the edited message content | AI response is appropriate and complete |

### Part 2: Agents Chat

| # | Action | Expected Result |
|---|--------|-----------------|
| 10 | Navigate to agents chat interface | Agents chat interface loads successfully |
| 11 | Select an active agent | Agent is selected and chat interface is ready |
| 12 | Type "Original message text" in the input field | Text appears in the input field |
| 13 | Click Send button | Message is sent and appears in the chat thread |
| 14 | Click Stop button during agent response processing | Stop button is clicked; message is removed from thread |
| 15 | Verify "Original message text" appears in the input field | Message is restored to the input field |
| 16 | Edit the message in the input field to read "Edited message text" | Text is successfully edited; input field responds to keyboard input |
| 17 | Click Send button to resend the edited message | Edited message "Edited message text" appears in the chat thread |
| 18 | Wait for agent response to complete | Agent response is generated for the edited message |
| 19 | Verify the agent response is relevant to the edited message content | Agent response is appropriate and complete |

## Expected Final State

Both regular chat and agents chat display the edited message ("Edited message text") in their respective threads with complete AI/agent responses. Original message text does not appear in either thread.

## Pass/Fail Criteria

**Pass:**
- Restored message is editable in both chat types
- Edited message is successfully sent in both chat types
- AI/agent responses are generated for the edited messages
- No errors or UI freezing occurs

**Fail:**
- Input field is not editable after restoration
- Edited message fails to send
- AI/agent responses are not generated
- Original message appears in the thread instead of edited version
