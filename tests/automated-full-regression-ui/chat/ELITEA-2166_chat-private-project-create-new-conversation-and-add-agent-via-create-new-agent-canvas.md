---
id: ELITEA-2166
title: "Chat – Private Project – Create New Conversation and Add Agent via Create New Agent Canvas"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:chat]
requirements: []
automation_test_id: tests.ui.chat.test_create_agent_via_chat_canvas.TestCreateAgentViaChatCanvas.test_create_new_conversation_and_add_agent_via_canvas
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/710
---

# ELITEA-2166: Chat – Private Project – Create New Conversation and Add Agent via Create New Agent Canvas

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify the complete flow of creating a new conversation in a Private project, creating a new agent via canvas, saving it, and sending a message that the agent responds to.

---

## Preconditions

- User is logged in to the Elitea platform.
- User is in a Private project.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent name | echo | Agent description | test agent | Instructions | echo every user input | Test message | hi |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats in Private project and click + Chat | New conversation opens; PARTICIPANTS panel empty; 'Invite Users' NOT in + menu |
| 2 | Click + icon, click Agents, click '+ Create New Agent' | Canvas panel opens showing Create New Agent form |
| 3 | Verify canvas sections: GENERAL (Name*, Description*, Tags), INSTRUCTIONS, WELCOME MESSAGE, CHAT STARTERS, ADVANCED | All sections visible |
| 4 | Verify Save button disabled when mandatory fields empty | Save button greyed out |
| 5 | Fill Name 'echo', Description 'test agent', INSTRUCTIONS 'echo every user input' | Fields filled |
| 6 | Verify Save button becomes active | Save button enabled |
| 7 | Click Save | Canvas transitions to saved agent view showing 'echo' and 'base' version |
| 8 | Verify message input bar shows 'echo | base' and PARTICIPANTS shows 'echo' under AGENTS | Agent is listed |
| 9 | Click X to close canvas | Canvas closes; conversation view shown |
| 10 | Type 'hi' and click Send | Message sent; agent responds; no errors |

---

## Expected Final State

New agent created via canvas and responds to messages.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Agent created, canvas closed, agent responds.

**Fail:**
- Any step produces an error or unexpected result.
- Agent not created or agent does not respond.
