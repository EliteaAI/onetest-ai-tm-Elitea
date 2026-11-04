---
id: ELITEA-4394
title: "Context Budget Counts Correctly When Deselecting Non-Pipeline Participant Types (Agent, Toolkit, MCP) Mid-Conversation"
priority: high
type: functional
module: context-management
status: draft
execution_type: manual
tags: [feat:chat, feat:context-management, feat:pipelines, issue:4840, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4840]
---
# ELITEA-4394: Context Budget Counts Correctly When Deselecting Non-Pipeline Participant Types (Agent, Toolkit, MCP) Mid-Conversation

**Module:** Context Management · **Priority:** High · **Type:** Functional

**Objective:** Verify the counting-logic change made for pipelines (issue #4840 fix) does not introduce a regression for other participant types sharing the same Context Budget widget and PARTICIPANTS panel — Agent, Toolkit, and MCP.

## Preconditions

- Logged in to {{base_url}}
- An Agent, a Toolkit, and an MCP are each available to add as chat participants
- The Context Budget widget is visible in Chat

## Test Data

| # | Participant Type |
|---|---|
| 1 | Agent |
| 2 | Toolkit |
| 3 | MCP |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Chat conversation and add an Agent as a participant. | Agent is added and appears correctly in PARTICIPANTS. |
| 2 | Select it, run it once, note Context Budget values. | Agent executes successfully; Context Budget values are recorded as baseline. |
| 3 | Deselect the Agent and send a normal message; check Messages/token count for inflation. | Messages/token count reflect only the expected increment — no inflated spike after deselecting the Agent. |
| 4 | Repeat Steps 1–3 using a Toolkit as the participant. | Toolkit shows the same correct, non-inflated behavior after deselect. |
| 5 | Repeat Steps 1–3 using an MCP as the participant. | MCP shows the same correct, non-inflated behavior after deselect. |
| 6 | For each participant type, send one more follow-up message and confirm values remain stable/correct (no delayed self-correction behavior). | Context Budget values remain stable and correct on the following message for Agent, Toolkit, and MCP — no delayed "self-correction" jump observed. |

## Expected Final State

Deselecting an Agent, Toolkit, or MCP participant mid-conversation does not cause any inflation or anomalous delayed correction of the Context Budget's Messages or token count — behavior remains consistent with the fixed pipeline counting logic.

## Pass/Fail Criteria

**Pass:**
- For all three participant types (Agent, Toolkit, MCP), Context Budget values after deselect + next message reflect only the expected increment.
- No delayed self-correction pattern appears on the subsequent message for any participant type.

**Fail:**
- Any of Agent, Toolkit, or MCP shows an inflated message/token count after being deselected and a message is sent.
- Values "self-correct" on a later message, indicating the same class of defect as #4840 has regressed into another participant type.
