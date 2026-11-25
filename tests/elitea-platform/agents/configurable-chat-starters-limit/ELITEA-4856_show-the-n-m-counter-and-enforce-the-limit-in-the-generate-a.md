---
id: ELITEA-4856
title: "Show the N/M counter and enforce the limit in the Generate Agent and Edit with AI modals"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}` as a platform admin
- An agent with 4 starters exists
- The original limit is noted (restore it at the end)

## Test Data

| Limit M | Modal | Expected |
|---------|-------|----------|
| 2 | Generate Agent (Build with AI) review step | "n/2 added."; adding stops at 2 with the at-limit tooltip |
| 2 | Edit with AI on the 4-starter agent | "n/2 added." in the over-limit state (n > 2); + disabled with the over-limit tooltip |
| 10 | Generate Agent | adding allowed up to "10/10 added.", then + disabled; Approve saves the 10 shown |
| 10 | Edit with AI on the 4-starter agent | under the limit; adding allowed up to "10/10 added." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set M = 2. Agents → + → Build with AI, enter a description and Generate | The review step shows a starters list with "n/2 added." (n ≤ 2) |
| 2 | Add starters until + is disabled; hover it | It stops at "2/2 added." with the at-limit tooltip |
| 3 | Close without saving. Open Edit with AI on the 4-starter agent and generate a draft | "n/2 added." in the over-limit state; + disabled with the over-limit tooltip |
| 4 | Close without saving | The agent still has 4 starters |
| 5 | Set M = 10 and repeat steps 1–2 | "n/10 added."; adding allowed up to "10/10 added.", then + disabled |
| 6 | Approve the Generate flow | The agent is created with the 10 shown starters in order; the editor reads "10/10" |
| 7 | Repeat step 3 with M = 10 | Under the limit; adding allowed up to "10/10 added." |
| 8 | Close without saving, delete the generated agent, restore the original limit | Cleaned up; the 4-starter agent is unchanged |

## Expected Final State

The AI modals follow M exactly as the editor does. Nothing changed except the agent created and deleted in step 6.

## Pass/Fail Criteria

**Pass:**
- Both modals show "n/M added." and enforce M with the same states and tooltips as the editor

**Fail:**
- A modal uses a hardcoded 4, allows adding past M, or saves different starters than it showed
