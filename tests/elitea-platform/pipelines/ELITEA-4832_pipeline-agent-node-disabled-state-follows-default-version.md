---
id: ELITEA-4832
title: "Pipeline Agent node - nesting disabled state follows the agent's default version"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, feat:pipeline_nodes, feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7085]
---
# ELITEA-4832: Pipeline Agent node - nesting disabled state follows the agent's default version

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that the nesting check uses the agent's **default** version. Making a shallow version the default makes the agent selectable, and switching back disables it again.

## Preconditions

- Logged in to {{base_url}}
- Agent **QA-A4** from ELITEA-4830: its **base** version is 4 tiers, so it's disabled
- **QA-A4** has a second saved version **v-shallow** with no sub-agents

## Test Data

| Version of QA-A4 | Depth |
|---|---|
| base | 4 tiers |
| v-shallow | 1 tier |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | With **base** as the default, open a pipeline, add an **Agent** node and open **Agents & Pipelines**. | **QA-A4** is greyed out with the nesting tooltip. |
| 2 | In another tab open **QA-A4** and set **v-shallow** as its default version. | The default version is changed. |
| 3 | Go back to the pipeline, reload the page and open the Agent node dropdown again. | **QA-A4** is enabled. |
| 4 | Select **QA-A4**. | The agent is selected, and **Version** shows **v-shallow**. |
| 5 | Set **base** back as the default version of **QA-A4**. Reload the pipeline and open the dropdown in a new Agent node. | **QA-A4** is greyed out again with the nesting tooltip. |

## Expected Final State

The agent's disabled state always matches the depth of its current default version.

## Pass/Fail Criteria

**Pass:** The agent is disabled only while its default version is too deep.
**Fail:** The state doesn't follow the default version, or a non-default version decides it.
