---
id: ELITEA-4829
title: "Pipeline Agent node - search finds the disabled Swarm Mode agent and keeps it disabled"
priority: critical
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, feat:pipeline_nodes, feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7085]
---
# ELITEA-4829: Pipeline Agent node - search finds the disabled Swarm Mode agent and keeps it disabled

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a disabled agent stays searchable in the Agent node dropdown and keeps its disabled state and tooltip in the search results. Before the fix, swarm agents were filtered out and search showed "No agents found".

## Preconditions

- Logged in to {{base_url}}
- Project **Bugs & Features** has the swarm agent **Swarm Coordinator**

## Test Data

| Field | Value |
|---|---|
| Search text 1 | `sw` |
| Search text 2 | `Swarm Coordinator` |
| Search text 3 | `coordinator` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open {{base_url}}, project **Bugs & Features**, **Explore → Pipelines**, open a pipeline. | Pipeline editor opens. |
| 2 | Click **+ Node** and add an **Agent** node. | The Agent node is added and its panel opens. |
| 3 | Open **Agents & Pipelines** and type `sw` in **Search agents and pipelines...** | The list is filtered. **Swarm Coordinator** is shown greyed out. Any other matching agent is enabled. "No agents found" isn't shown. |
| 4 | Hover over **Swarm Coordinator** in the results. | The Swarm tooltip from ELITEA-4828 is shown. |
| 5 | Click **Swarm Coordinator** in the results. | Nothing is selected; the node stays **Not configured**. |
| 6 | Change the search to `Swarm Coordinator`, then to `coordinator`. | **Swarm Coordinator** is found each time, stays greyed out and keeps the tooltip. |
| 7 | Clear the search. | The full list returns; **Swarm Coordinator** is still greyed out. |

## Expected Final State

The swarm agent is found by every search and is never selectable.

## Pass/Fail Criteria

**Pass:** Search returns the swarm agent as a disabled row with the tooltip, and "No agents found" never appears for it.
**Fail:** Search hides the agent, shows "No agents found", or shows it as enabled or selectable.
