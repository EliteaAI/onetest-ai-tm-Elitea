---
id: ELITEA-2092
title: "Create New Conversation via Agent HUB — Start Conversation (No Conversation Starters)"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2092: Create New Conversation via Agent HUB — Start Conversation (No Conversation Starters)

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that starting a conversation from Agent HUB with an agent that has no conversation starters opens the chat with the agent pre-loaded and the agent responds correctly.

---

## Preconditions

- User is logged in to the Elitea platform.
- User is in a Private project.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent name | Business Analyst |
| First message | hi |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Agent HUB from the left sidebar | Agent HUB page opens |
| 2 | Click on an agent card with no conversation starters (e.g. "Business Analyst") | Detail modal opens with agent info |
| 3 | Verify the CONVERSATION STARTERS section displays "No predefined conversation starters — just type your request to begin" | No starter buttons shown |
| 4 | Click the "Start conversation" button | Modal closes; Chat opens with agent pre-loaded |
| 5 | Verify the input bar displays the Agent name and version (e.g. "Business Analyst v2.1") and an × button | Agent chip shown |
| 6 | Type "hi" and click Send | Agent processes and responds; agent name shown as respondent |
| 7 | Verify a new entry appears in Today with "Naming…" placeholder that resolves to auto-generated title | Conversation auto-named |

---

## Expected Final State

Conversation started from Agent HUB with agent pre-loaded; agent responds; conversation auto-named.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Agent is pre-loaded, responds, and conversation is auto-named.

**Fail:**
- Any step produces an error or unexpected result.
- Agent is not loaded or conversation fails to auto-name.
