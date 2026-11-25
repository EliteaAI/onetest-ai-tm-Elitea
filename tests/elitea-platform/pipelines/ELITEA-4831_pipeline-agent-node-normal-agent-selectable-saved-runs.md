---
id: ELITEA-4831
title: "Pipeline Agent node - normal agent is selectable, saved and runs (regression for disabled agents)"
priority: critical
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, feat:pipeline_nodes, feat:agents, rca:regression, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7085]
---
# ELITEA-4831: Pipeline Agent node - normal agent is selectable, saved and runs (regression for disabled agents)

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that agents without Swarm Mode and within the nesting limit aren't greyed out, and still work end to end in a pipeline Agent node.

## Preconditions

- Logged in to {{base_url}}
- Project **Bugs & Features** has normal agents (e.g. **Multipurpose**, **PDF Review Assistant**, **SDE**) and the swarm agent **Swarm Coordinator**

## Test Data

| Field | Value |
|---|---|
| Agent | Multipurpose |
| Task type / value | F-String / `Say hello` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open {{base_url}}, project **Bugs & Features**, **Explore → Pipelines**, open a pipeline (e.g. a new one). | Pipeline editor opens. |
| 2 | Click **+ Node** and add an **Agent** node. | The Agent node is added with **Not configured**. |
| 3 | Open **Agents & Pipelines** and look at the normal agents. Hover over a few. | Normal agents aren't greyed out and show no disabled tooltip. |
| 4 | Select **Multipurpose**. | **Multipurpose** is shown, **Version** = **base**, and the left panel **TOOLS** shows **Multipurpose · base · Used by Agent 1**. The node still shows **Not configured** (task value is empty). |
| 5 | In **TASK** set Type **F-String** and Value `Say hello`. Connect the node's **Output** to **End**. Make the Agent node the entrypoint (or connect it after the existing entrypoint node) and click **Save**. | The node no longer shows **Not configured**, and the pipeline is saved. |
| 6 | Reload the page and open the Agent node. | **Multipurpose**, its version and the task are kept. |
| 7 | Click **Test Pipeline** (or run the pipeline in a chat). | The run completes, the Agent node returns the agent's answer, and no error appears. |
| 8 | Add a second Agent node and open its **Agents & Pipelines** dropdown. | Same states as the first node: **Swarm Coordinator** is disabled and normal agents are enabled. |

## Expected Final State

The pipeline with a normal agent in the Agent node is saved and runs successfully.

## Pass/Fail Criteria

**Pass:** Normal agents are enabled in every Agent node, and the selected agent saves, persists and runs.
**Fail:** A normal agent is greyed out, can't be selected, is lost after reload, or the run fails.
