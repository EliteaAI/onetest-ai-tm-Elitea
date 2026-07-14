---
id: ELITEA-1886
title: "Conversation starter chips appear in chat panel and are clickable"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
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
| 4 | Open a new chat session with this agent | A new chat session opens |
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
