---
id: ELITEA-1006
title: "Chat Input and Send Button Blocked During Pending Authorization"
priority: high
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1006: Chat Input and Send Button Blocked During Pending Authorization

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that the chat input field and Send button are disabled while the authorization dialog is displayed, preventing new messages from being submitted.

## Preconditions

- Authorization dialog is currently visible in the agent chat

## Test Data

- Input text to attempt: 'Test message while blocked'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Observe the chat input field while the authorization dialog is displayed. | Input field appears visually inactive (grayed out or disabled indicator). |
| 2 | Observe the Send button while the authorization dialog is displayed. | Send button appears disabled and cannot be clicked. |
| 3 | Click into the chat input field and try to type. | Input field does not accept keyboard input, OR input is visible but pressing Enter does not send. |
| 4 | Click the Send button directly (attempt to bypass). | No message is submitted. The action is ignored. |
| 5 | Click [Authorize] on the dialog. | Dialog closes. |
| 6 | Observe the chat input field and Send button after Authorize. | Both become active and functional. |
| 7 | Trigger the tool again to show the dialog. Click [Block]. | Dialog closes. |
| 8 | Observe the chat input field and Send button after Block. | Both become active and functional. |

## Expected Final State

Both become active and functional.

## Pass/Fail Criteria

Pass:
- Input field accepts no text (or cannot submit) while dialog is open
- Send button is non-functional while dialog is open
- Both input and Send re-enable immediately after Authorize or Block

Fail:
- User can type and submit a new message while the dialog is open
- Input or Send remain disabled after dialog is dismissed
