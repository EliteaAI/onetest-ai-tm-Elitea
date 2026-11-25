---
id: ELITEA-4828
title: "Pipeline Agent node - Swarm Mode agent is listed disabled with tooltip and cannot be selected"
priority: critical
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, feat:pipeline_nodes, feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7085]
---
# ELITEA-4828: Pipeline Agent node - Swarm Mode agent is listed disabled with tooltip and cannot be selected

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an agent with Swarm Mode enabled is shown greyed out in the Agent node's **Agents & Pipelines** dropdown, explains why on hover, and cannot be selected.

## Preconditions

- Logged in to {{base_url}}
- Project **Bugs & Features** has an agent with **Swarm Mode** enabled (e.g. **Swarm Coordinator**) and at least one normal agent (e.g. **Multipurpose**)

## Test Data

| Field | Value |
|---|---|
| Project | Bugs & Features |
| Swarm agent | Swarm Coordinator |
| Normal agent | Multipurpose |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open {{base_url}}, select project **Bugs & Features**. In the left menu click **Explore → Pipelines** and open a pipeline (or create one). | Pipeline editor opens on the **Flow** tab. |
| 2 | Click **+ Node** and add an **Agent** node. | The Agent node appears on the canvas with **Not configured**; the right panel opens with **BASIC → Agents & Pipelines**. |
| 3 | Click the **Agents & Pipelines** dropdown. | The list opens with **Search agents and pipelines...**, **Create new agent**, **Create new pipeline**, then the project agents and pipelines, each with icon, name and a truncated description. |
| 4 | Scroll to **Swarm Coordinator**. | **Swarm Coordinator** is listed (not hidden). Its icon, name and description are greyed out. Normal agents (e.g. **Multipurpose**) are not greyed out. |
| 5 | Hover over **Swarm Coordinator**. | A tooltip is shown next to the row and doesn't hide the row text. Text is exactly: "The Swarm Coordinator agent has Swarm Mode enabled and can't be added as a tool. Swarm agents are only supported in direct chat." |
| 6 | Click **Swarm Coordinator**. | Nothing is selected: the dropdown value doesn't change, the node stays **Not configured**, no toast appears, and the list stays usable. |
| 7 | Move to **Swarm Coordinator** with the keyboard arrows and press **Enter**. | Nothing is selected, as in step 6. |
| 8 | Select **Multipurpose**. | **Multipurpose** is shown in the dropdown, a **Version** field (**base**) and the **TASK** section (Type **F-String**, empty **Value**) appear, and **TOOLS** in the left panel shows **Multipurpose · base · Used by Agent 1**. The node still shows **Not configured** until the task value is filled in. |

## Expected Final State

The swarm agent stays visible but disabled with the exact tooltip. Only the normal agent can be bound to the node.

## Pass/Fail Criteria

**Pass:** The swarm agent is listed, greyed out, shows the exact tooltip and can't be selected by mouse or keyboard. Normal agents select normally.
**Fail:** The swarm agent is hidden, looks enabled, has no or a different tooltip, or can be selected; or a normal agent is shown as disabled.
