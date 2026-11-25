---
id: ELITEA-4830
title: "Pipeline Agent node - agent whose default version nests more than 3 tiers is disabled with nesting tooltip; 3 tiers can be selected"
priority: critical
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, feat:pipeline_nodes, feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7085]
---
# ELITEA-4830: Pipeline Agent node - agent whose default version nests more than 3 tiers is disabled with nesting tooltip; 3 tiers can be selected

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the nesting-depth rule in the pipeline Agent node. The pipeline host consumes 0 tiers, so an agent with a 3-tier chain can be selected, and an agent with a 4-tier chain is disabled with the nesting tooltip.

## Preconditions

- Logged in to {{base_url}}
- Test agents in **Bugs & Features** without Swarm Mode (names are examples). Build each chain on the **base** version, from the bottom up, and save:
  - 3 tiers: add **QA-C** to **QA-B** as a tool, then **QA-B** to **QA-A**. **QA-A** = A→B→C.
  - 4 tiers: build **QA-A4** → **QA-B4** → **QA-C4** the same way, then add **QA-D4** to **QA-C4**. **QA-A4** = A4→B4→C4→D4.
- If the agent editor blocks building the 4-tier chain, record that in the run and ask dev for a 4-tier test agent.

## Test Data

| Agent | Default version depth | Expected in Agent node |
|---|---|---|
| QA-A | 3 tiers | Enabled |
| QA-A4 | 4 tiers | Disabled |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open {{base_url}}, project **Bugs & Features**, **Explore → Pipelines**, open a pipeline. | Pipeline editor opens. |
| 2 | Click **+ Node** and add an **Agent** node. | The Agent node is added and its panel opens. |
| 3 | Open **Agents & Pipelines** and search `QA-A4`. | **QA-A4** is listed greyed out. |
| 4 | Hover over **QA-A4**. | Tooltip shows exactly: "The default version of QA-A4 nests agents too deeply: agent nesting is limited to 3 tiers (orchestrator → sub-orchestrator → leaf). Make a shallower version its default to add it." |
| 5 | Click **QA-A4**. | Nothing is selected, the node stays **Not configured**, and no toast appears. |
| 6 | Change the search to `QA-A`. Check both rows, then select **QA-A**. | Both **QA-A** and **QA-A4** are listed; **QA-A4** is greyed out and **QA-A** isn't. **QA-A** is selected, **Version** shows its default version, and no error toast appears. |
| 7 | In **TASK** set Type **F-String** and Value `Say hello`. Click **Save**, reload the page and open the Agent node. | The pipeline is saved, and the node still shows **QA-A** with the task value. |

## Expected Final State

The 3-tier agent is bound to the Agent node. The 4-tier agent can't be bound and the tooltip explains why.

## Pass/Fail Criteria

**Pass:** The 4-tier agent is disabled with the exact nesting tooltip, and the 3-tier agent selects and saves.
**Fail:** The 4-tier agent can be selected or only fails with a toast after the click; the 3-tier agent is disabled; or the tooltip text differs.
