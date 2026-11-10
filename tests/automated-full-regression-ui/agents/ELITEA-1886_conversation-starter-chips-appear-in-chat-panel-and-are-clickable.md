---
id: ELITEA-1886
title: "Conversation starter chips appear in chat panel and are clickable"
priority: medium
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id:
  - tests.ui.agents.test_agent_embedded_chat_conversation_starter_chips.TestConversationStarterChipsVisibleAndClickable.test_conversation_starter_chips_visible_and_clickable
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1292
---

# ELITEA-1886: Conversation starter chips appear in chat panel and are clickable

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that conversation starter chips configured for an agent are visible in the chat panel before any message is sent, and that clicking a chip pre-fills the input and triggers an agent response.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent is available.

---

## Test Data

| Field | Value |
|-------|-------|
| Starter 1 | How do I create a new agent? |
| Starter 2 | What toolkits are available? |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page | The agent detail page loads |
| 2 | Add starter "How do I create a new agent?" and starter "What toolkits are available?" | Both starters are entered in the Conversation Starters field |
| 3 | Click Save | Save completes successfully |
| 4 | Click the "Test Agent" toolbar button to open the embedded chat panel (new chat session with this agent) | The chat panel opens with a new chat session |
| 5 | Verify both starter chips are visible in the chat before any message is sent | Both starter chip buttons are displayed in the chat panel |
| 6 | Click one starter chip | The starter chip is clicked |
| 7 | Verify the starter text is submitted as a pre-filled in the input | The starter text appears in the chat input field |
| 8 | Verify the agent responds to the clicked starter | An agent response is rendered in the chat panel |

---

## Expected Final State

Both conversation starter chips are visible before any message, and clicking one pre-fills the input with the starter text and triggers an agent response.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Starter chips are visible, clickable, pre-fill the input, and trigger agent responses.

**Fail:**
- Any step produces an error or unexpected result.
- Starter chips are absent, not clickable, do not pre-fill the input, or no response is triggered.
