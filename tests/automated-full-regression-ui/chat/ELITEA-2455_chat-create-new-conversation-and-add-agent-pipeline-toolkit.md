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
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/8b713c60
---

# ELITEA-2455: Chat – Create new conversation and add Agent, Pipeline, Skill, Toolkit, and MCP as participants

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
| 5 | Verify a popup menu opens with options: Attach Files (showing "10 left"), Modules, Agents, Pipelines, Skills, Toolkits, MCPs (Invite Users only outside a private project) | The plus menu lists all of these options, including Skills. |
| 6 | Click Agents, verify a dropdown list opens with a search field and a "Create Agent" option plus a list of available agents | The dropdown opens on click; search, Create Agent and the agent list are shown. |
| 7 | Select any agent from the list and verify the agent with the selected name is added to the AGENTS section of the PARTICIPANTS panel with name, version, and icon | The entity with the selected name appears as a participant in the AGENTS section (the specific agent name is not prescribed). |
| 8 | Click + again, click Pipelines, verify a dropdown with "Create Pipeline" and available pipelines | The dropdown opens on click with Create Pipeline and the pipeline list. |
| 9 | Select any pipeline and verify the pipeline with the selected name is added to the PIPELINES section of the PARTICIPANTS panel | The entity with the selected name appears in the PIPELINES section (name not prescribed). |
| 9a | Click + again, click Skills, verify a dropdown with "Create Skill" and available skills; select any skill and verify the skill with the selected name is added to the SKILLS section of the PARTICIPANTS panel | The dropdown opens on click; the entity with the selected name appears in the SKILLS section (name not prescribed). |
| 10 | Click + again, click Toolkits, verify a dropdown with toggle switches for each toolkit | Control responds; expected next state is shown. |
| 11 | Enable a toolkit by clicking its toggle switch (any toolkit) and verify the toolkit with that name appears in the TOOLKITS section of the PARTICIPANTS panel | The entity with the selected name appears in the TOOLKITS section (name not prescribed). |
| 12 | Click + again, click MCPs, verify a dropdown with toggle switches for each MCP | Control responds; expected next state is shown. |
| 13 | Enable any MCP and verify the MCP with that name appears in the MCPS section of the PARTICIPANTS panel | The entity with the selected name appears in the MCPS section (name not prescribed). |
| 14 | Verify all four sections are visible in order in the PARTICIPANTS panel: AGENTS, PIPELINES, SKILLS, TOOLKITS, MCPS | Condition holds as described. |
| 15 | Verify each participant type shows a distinct icon (agent icon, pipeline icon, skill icon, toolkit icon, MCP icon) | Condition holds as described. |
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
