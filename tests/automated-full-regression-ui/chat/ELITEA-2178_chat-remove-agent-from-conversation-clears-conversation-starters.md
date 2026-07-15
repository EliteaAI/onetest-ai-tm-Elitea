---
id: ELITEA-2178
title: "Chat – Remove Agent from Conversation Clears Conversation Starters"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2178: Chat – Remove Agent from Conversation Clears Conversation Starters

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that removing an agent from a conversation also removes the conversation starter buttons and restores the default LLM.

---

## Preconditions

- User is logged in to the Elitea platform.
- A conversation with an agent that has conversation starters exists.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent name | Claude B |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Verify agent 'Claude B' is in the conversation with starters visible | Agent chip and starters shown |
| 2 | In PARTICIPANTS AGENTS section, hover over trash bin icon next to agent | 'Remove agent' tooltip appears |
| 3 | Click the trash bin icon | 'Remove agent?' modal appears |
| 4 | Verify modal text: 'Are you sure to remove the Claude B agent from conversation?' | Modal text correct |
| 5 | Click Remove | Modal closes; AGENTS section removed from PARTICIPANTS; default LLM restored in input bar |
| 6 | Verify conversation starters no longer displayed | Starters gone |
| 7 | Verify conversation history intact | Previous messages still visible |

---

## Expected Final State

Agent removed; starters cleared; default LLM restored; history intact.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Agent removal clears starters and restores default LLM.

**Fail:**
- Any step produces an error or unexpected result.
- Starters remain or LLM not restored.
