---
id: ELITEA-0565
title: "Restore Conversation Closes History Tab and Displays Chat"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:pipelines, rca:regression, eng:frontend, feat:agents, r-2.0.1, ui]
requirements: [ProjectAlita/projectalita.github.io#3928]
---
# ELITEA-0565: Restore Conversation Closes History Tab and Displays Chat

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking "Restore Conversation" in the History tab automatically closes the History tab and navigates the user to the restored chat view, for both Agents and Pipelines.

**Coverage:**
- Clicking "Restore Conversation" dismisses/closes the History tab
- The restored chat conversation is immediately displayed in the chat view without any manual action
- Behavior is consistent for both Agent and Pipeline history entries
- No ambiguity left for the user as to whether restore succeeded

## Preconditions

- User is logged in to the ELITEA platform
- Environment: {{base_url}}
- Browser: Chrome (latest stable)
- At least one previously executed Agent with conversation history exists
- At least one previously executed Pipeline with conversation history exists

## Test Data

| Entity Type | Example | Pre-existing history required |
|---|---|---|
| Agent | Any agent with at least 1 prior run in History | Yes |
| Pipeline | Any pipeline with at least 1 prior run in History | Yes |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents page from the sidebar. Open any agent that has prior execution history. | Agent page opens successfully. |
| 2 | Click the History tab (or open the History panel) for the agent. | The History tab opens and displays a list of previously executed conversations. |
| 3 | Locate any conversation entry in the history list. Click 'Restore Conversation' on it. | The History tab closes automatically AND the restored conversation is displayed in the chat view without any manual intervention. |
| 4 | Verify the chat view content matches the restored conversation (messages are visible). | Chat messages from the restored session are correctly displayed. |
| 5 | Navigate to the Pipelines page from the sidebar. Open any pipeline that has prior execution history. | Pipeline page opens successfully. |
| 6 | Click the History tab for the pipeline. | The History tab opens and displays a list of previously executed conversations. |
| 7 | Locate any conversation entry. Click 'Restore Conversation' on it. | The History tab closes automatically AND the restored conversation is displayed in the chat view without manual intervention. |
| 8 | Verify the chat view content matches the restored conversation. | Chat messages from the restored session are correctly displayed. |

## Expected Final State

Chat messages from the restored session are correctly displayed.

## Pass/Fail Criteria

**Pass:**
- After clicking "Restore Conversation", the History tab closes automatically for both Agent and Pipeline
- The restored chat conversation is rendered in the chat view immediately, without requiring the user to manually close the History tab
- The content of the restored chat matches the previously executed session

**Fail:**
- The History tab remains open after clicking "Restore Conversation"
- The user must manually close the History tab to see the restored chat
- No chat content is displayed, or an error is shown
- Behavior differs between Agent and Pipeline (one works, one doesn't)
