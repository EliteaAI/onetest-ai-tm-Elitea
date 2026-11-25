---
id: ELITEA-4833
title: "Pipeline Agent node - toggling Swarm Mode changes availability; Swarm reason wins over nesting"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, feat:pipeline_nodes, feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7085]
---
# ELITEA-4833: Pipeline Agent node - toggling Swarm Mode changes availability; Swarm reason wins over nesting

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that turning Swarm Mode off and on updates the agent's availability in the Agent node dropdown, and that an agent that is both swarm and too deep shows only the Swarm tooltip.

## Preconditions

- Logged in to {{base_url}}
- An editable test agent **QA-Swarm-Toggle** with no sub-agents
- Agent **QA-A4** from ELITEA-4830 (4 tiers)

## Test Data

| Agent | Swarm Mode | Depth |
|---|---|---|
| QA-Swarm-Toggle | on → off → on | 1 tier |
| QA-A4 | on (temporarily) | 4 tiers |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Turn **Swarm Mode** on for **QA-Swarm-Toggle** and save. Open a pipeline, add an **Agent** node and open **Agents & Pipelines**. | **QA-Swarm-Toggle** is greyed out with the tooltip "The QA-Swarm-Toggle agent has Swarm Mode enabled and can't be added as a tool. Swarm agents are only supported in direct chat." |
| 2 | Turn **Swarm Mode** off for **QA-Swarm-Toggle** and save. Reload the pipeline and open the dropdown. | **QA-Swarm-Toggle** is enabled and can be selected. |
| 3 | Turn **Swarm Mode** on again and save. Reload the pipeline and open the dropdown in a new Agent node. | **QA-Swarm-Toggle** is greyed out again. |
| 4 | Turn **Swarm Mode** on for **QA-A4** and save. Open the dropdown and hover over **QA-A4**. | Only the Swarm tooltip ("The QA-A4 agent has Swarm Mode enabled and can't be added as a tool. Swarm agents are only supported in direct chat.") is shown, not the nesting tooltip. |
| 5 | Clean up: turn Swarm Mode off for **QA-A4** and **QA-Swarm-Toggle**. | Both agents are back to their earlier state (**QA-A4** is again disabled with the nesting tooltip only). |

## Expected Final State

Availability follows the agent's Swarm Mode setting, and Swarm is the reason shown when both reasons apply.

## Pass/Fail Criteria

**Pass:** The disabled state changes with Swarm Mode after reload, and the combined case shows only the Swarm tooltip.
**Fail:** The state doesn't update, or the combined case shows the nesting tooltip or both.
