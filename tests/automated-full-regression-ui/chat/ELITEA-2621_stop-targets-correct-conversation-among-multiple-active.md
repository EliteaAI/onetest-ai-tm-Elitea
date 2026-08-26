---
id: ELITEA-2621
title: "Chat – Stop Targets the Correct Conversation When Multiple Are Active"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, eng:backend, issue:5196]
requirements: [EliteaAI/elitea_issues#5196]
---

# ELITEA-2621: Chat – Stop Targets the Correct Conversation When Multiple Are Active

**Module:** chat-interface / streaming · **Priority:** High · **Type:** Functional

**Objective:** Verify that stopping generation in one conversation only interrupts that conversation's task, and does not affect a different conversation with an in-flight generation (e.g. main Chat vs. Support Assistant widget, or two separate chat conversations open in different tabs).

---

## Preconditions

- User is logged in to the Elitea platform.
- Two separate active generations can be started concurrently — e.g. one in the main Chat module and one in the Support Assistant widget, or two different conversations open in two browser tabs.

---

## Test Data

| Field | Value |
|-------|-------|
| Conversation A message | "generate a long story about space travel" |
| Conversation B message | "generate a long story about the ocean" |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | In Conversation A, send the message and confirm generation/thinking is in progress | Conversation A is streaming/thinking; Stop visible |
| 2 | In Conversation B (different tab/widget), send its message and confirm generation/thinking is in progress | Conversation B is streaming/thinking; Stop visible |
| 3 | In Conversation A, click Stop | Conversation A's generation halts; input restored in A |
| 4 | Switch to Conversation B | Conversation B is still actively streaming/thinking, unaffected |
| 5 | Let Conversation B's response complete naturally | Conversation B produces a full, uninterrupted response |

---

## Expected Final State

Stopping Conversation A does not interrupt or affect Conversation B's independent generation; each stop request targets only its own conversation/task.

---

## Pass/Fail Criteria

**Pass:**
- Stop in Conversation A only halts Conversation A.
- Conversation B continues to completion unaffected.

**Fail:**
- Stopping Conversation A also halts or corrupts Conversation B's generation.
- Cross-talk between the two conversations' stop/streaming state is observed.
