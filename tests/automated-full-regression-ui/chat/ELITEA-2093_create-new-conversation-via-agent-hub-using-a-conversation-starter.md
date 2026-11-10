---
id: ELITEA-2093
title: "Create New Conversation via Catalog — Using a Conversation Starter"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2093: Create New Conversation via Catalog — Using a Conversation Starter

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that selecting a conversation starter in the Catalog modal opens the chat with the starter text pre-populated and the agent responds correctly after sending.

---

## Preconditions

- User is logged in to the Elitea platform.
- User is in a Private project.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent name | Assistant for ELITEA Documentation |
| Conversation starter | Tell me about Elitea |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Catalog from the left sidebar | Catalog page opens |
| 2 | Click on an agent card with predefined conversation starters (e.g. "Assistant for ELITEA Documentation") | Detail modal opens |
| 3 | Verify CONVERSATION STARTERS section shows clickable starter buttons | Starter buttons visible |
| 4 | Click the "Tell me about Elitea" starter button | Modal closes; Chat opens with agent pre-loaded |
| 5 | Verify the selected starter text is pre-populated in the message input field | Starter text is in the input field |
| 6 | Verify the agent name and version are in the input bar and all three starter prompts are displayed as clickable suggestions | Agent chip and starters visible |
| 7 | Click the Send button | Pre-populated message is sent; agent responds |
| 8 | Verify a new entry appears in Today with "Naming…" placeholder that resolves to an auto-generated title | Conversation auto-named |

---

## Expected Final State

Conversation opened with starter text pre-populated; agent responds; conversation auto-named.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Starter text pre-populates, agent responds, conversation auto-named.

**Fail:**
- Any step produces an error or unexpected result.
- Starter text not pre-populated or agent fails to respond.
