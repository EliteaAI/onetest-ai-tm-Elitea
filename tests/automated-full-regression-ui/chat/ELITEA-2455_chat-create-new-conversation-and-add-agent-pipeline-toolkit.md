---
id: ELITEA-2455
title: "Chat – Create new conversation and add Agent, Pipeline, Toolkit, and MCP as participants"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:chat]
requirements: []
automation_test_id: [tests.ui.chat.test_new_conversation_add_participants.TestNewConversationParticipants.test_new_conversation_add_four_participant_types]
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/df8e5edf
---

# ELITEA-2455: Chat – Create new conversation and add Agent, Pipeline, Toolkit, and MCP as participants

**Module:** chat-interface · **Priority:** critical · **Type:** functional

**Objective:** Verify that Chat – Create new conversation and add Agent, Pipeline, Toolkit, and MCP as participants. Success is confirmed when verify any misconfigured entities display a yellow warning indicator.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Chats section and click the + Chat button | Target page/section loads successfully. |
| 2 | Verify a new conversation is created with "Type your message..." placeholder in the input field | Condition holds as described. |
| 3 | Verify the PARTICIPANTS panel is visible on the right and initially shows no participants | Condition holds as described. |
| 4 | Click the + icon at the bottom left of the message input area | Control responds; expected next state is shown. |
| 5 | Verify a popup menu opens with options: Attach Files (showing "10 left"), Modules, Agents, Pipelines, Toolkits, MCPs, Invite Users | Condition holds as described. |
| 6 | Click Agents, verify a submenu opens with a search field and "+ Create New Agent" option plus a list of available agents | Control responds; expected next state is shown. |
| 7 | Select an agent (e.g. "agent") and verify it appears in the AGENTS section of the PARTICIPANTS panel with name, version, and icon | Control responds; expected next state is shown. |
| 8 | Click + again, click Pipelines, verify a submenu with "+ Create New Pipeline" and available pipelines | Control responds; expected next state is shown. |
| 9 | Select a pipeline (e.g. "ALL Pipeline Nodes") and verify it appears in the PIPELINES section of the PARTICIPANTS panel | Control responds; expected next state is shown. |
| 10 | Click + again, click Toolkits, verify a submenu with toggle switches for each toolkit | Control responds; expected next state is shown. |
| 11 | Enable a toolkit by clicking its toggle switch (e.g. "storage") and verify it appears in the TOOLKITS section of the PARTICIPANTS panel | Action completes without error and produces the expected UI state. |
| 12 | Click + again, click MCPs, verify a submenu with toggle switches for each MCP | Control responds; expected next state is shown. |
| 13 | Enable an MCP (e.g. "Aha!") and verify it appears in the MCPS section of the PARTICIPANTS panel | Action completes without error and produces the expected UI state. |
| 14 | Verify all four sections are visible in order in the PARTICIPANTS panel: AGENTS, PIPELINES, TOOLKITS, MCPS | Condition holds as described. |
| 15 | Verify each participant type shows a distinct icon (agent icon, pipeline icon, toolkit icon, MCP icon) | Condition holds as described. |
| 16 | Verify no duplicate entries appear and no error messages are displayed | Condition holds as described. |
| 17 | Type "Hi" in the message field and click Send | Field accepts the input and displays the entered value. |
| 18 | Verify the conversation is created and the owner icon is added in the PARTICIPANTS panel | Condition holds as described. |
| 19 | Verify all added participants are visible under their respective type sections | Condition holds as described. |
| 20 | Verify any misconfigured entities display a yellow warning indicator | Condition holds as described. |

---

## Expected Final State

Verify any misconfigured entities display a yellow warning indicator.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – Create new conversation and add Agent, Pipeline, Toolkit, and MCP as participants.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
