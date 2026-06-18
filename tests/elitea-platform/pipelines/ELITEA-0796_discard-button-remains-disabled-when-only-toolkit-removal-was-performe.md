---
id: ELITEA-0796
title: "Discard Button Remains Disabled When Only Toolkit Removal Was Performed"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5105]
---
# ELITEA-0796: Discard Button Remains Disabled When Only Toolkit Removal Was Performed

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Discard button stays inactive (disabled) when the only change made to a pipeline is removing a toolkit from a Toolkit Node or LLM Node, because toolkit removal is an immediate irreversible operation not tracked in the save/discard cycle.

**Coverage:**
- Discard button is disabled after toolkit removal in Toolkit Node (no other changes)
- Discard button is disabled after toolkit removal in LLM Node (no other changes)
- Behavior is consistent with the documented design: toolkit removal does not activate the Discard flow

## Preconditions

- Logged in to {{base_url}}
- Two saved pipelines available: one with a Toolkit Node with a configured toolkit, one with an LLM Node with a configured toolkit
- Both pipelines start with Save and Discard disabled (no pending changes)

## Test Data

- Toolkit Node pipeline: Toolkit = Sharepoint, Tool = remove_index
- LLM Node pipeline: Toolkit = Artifacts / Artifactregression

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline with the Toolkit Node. Confirm Save and Discard are both disabled. | Save: disabled. Discard: disabled. |
| 2 | In the Toolkit Node, click the × / remove button to remove the toolkit (Sharepoint). | Toolkit is removed from the node. Save and Discard remain disabled — toolkit removal is auto-saved to the backend immediately and does not create a pending reversible change. |
| 3 | Observe the Discard button. | Discard button remains disabled. There is nothing to discard — toolkit removal is already committed. |
| 4 | Navigate away without clicking Save. Re-open the pipeline. | Pipeline loads with the toolkit already gone — the removal was auto-saved at the moment it happened, not dependent on Save or Discard. |
| 5 | Open the pipeline with the LLM Node. Confirm Save and Discard are both disabled. | Save: disabled. Discard: disabled. |
| 6 | In the LLM Node Toolkits section, remove the configured toolkit (Artifacts). | Toolkit entry is removed. Save and Discard remain disabled. |
| 7 | Observe the Discard button. | Discard button remains disabled. |

## Expected Final State

Discard button remains disabled.

## Pass/Fail Criteria

**Pass:**
- Discard button remains disabled after toolkit removal in both Toolkit Node and LLM Node scenarios
- Save button also remains inactive — no pending changes after toolkit removal
- Navigating away and returning shows the toolkit as already removed (auto-saved)

**Fail:**
- Discard or Save button becomes active after toolkit-only removal
- Navigating away and returning causes the toolkit to reappear (removal was not persisted)
