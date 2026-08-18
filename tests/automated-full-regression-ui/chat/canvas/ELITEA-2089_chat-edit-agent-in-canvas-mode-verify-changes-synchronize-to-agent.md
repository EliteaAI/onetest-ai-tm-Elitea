---
id: ELITEA-2089
title: "Chat – Edit Agent in Canvas Mode – Verify Changes Synchronize to Agent"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: tests.ui.chat.test_chat_canvas_edit_agent.TestChatCanvasEditAgent.test_edit_agent_welcome_message_syncs_to_agents_section
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1580
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2089: Chat – Edit Agent in Canvas Mode – Verify Changes Synchronize to Agent

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that editing an agent's Welcome Message through the chat canvas and saving the changes correctly synchronizes the update to the agent's configuration in the Agents section.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation with an agent named "echo" attached as a participant.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent name | echo |
| New welcome message | edited from canvas |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats and open a conversation with agent "echo base" in PARTICIPANTS | Conversation with agent is displayed |
| 2 | Click the pencil/edit icon next to "echo base" in the PARTICIPANTS section | Agent canvas opens with "echo" and "base" version tag |
| 3 | Verify the agent chip at the bottom shows "echo base Editing..." status | Editing state is indicated |
| 4 | Locate the WELCOME MESSAGE section in the canvas | Welcome Message section is visible |
| 5 | Click into the WELCOME MESSAGE text field | Field becomes editable |
| 6 | Type "edited from canvas" | Text "edited from canvas" appears in the field |
| 7 | Verify "Save" and "Discard" buttons become active | Buttons are now clickable |
| 8 | Click the "Save" button | Success notification: "The agent has been updated" appears |
| 9 | Close the canvas by clicking the X button | Canvas closes; conversation view is displayed |
| 10 | Verify the agent chip no longer shows "Editing..." status | Chip updated |
| 11 | Navigate to the Agents section from the left sidebar | Agents page opens |
| 12 | Locate and click on the "echo" agent | Agent details/canvas opens |
| 13 | Scroll down to the WELCOME MESSAGE section | Welcome Message section is visible |
| 14 | Verify the WELCOME MESSAGE field displays "edited from canvas" | Change is synchronized to agent |

---

## Expected Final State

The welcome message change made in the chat canvas is synchronized and saved to the agent's configuration in the Agents section.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Welcome message change is saved and visible in both chat canvas and Agents section.

**Fail:**
- Any step produces an error or unexpected result.
- Change is not saved or not reflected in the Agents section.
