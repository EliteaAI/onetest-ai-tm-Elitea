---
id: ELITEA-0796
title: "Toolkit Removal Alone Enables Discard, and Discard Restores the Toolkit"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.3, epic:7093]
requirements: [EliteaAI/elitea_issues#5105, EliteaAI/elitea_issues#7159]
---
# ELITEA-0796: Toolkit Removal Alone Enables Discard, and Discard Restores the Toolkit

> **Updated for Pipelines 2.0:** Behaviour change (#7159). Toolkit removal is no longer auto-saved: removing a toolkit (X) is an unsaved change that enables Save and Discard. Discard restores it, and navigating away without saving does not persist the removal.

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that removing a toolkit from a Toolkit Node or LLM Node (with no other changes) enables Save and Discard, that Discard restores the toolkit, and that the removal is persisted only on Save.

**Coverage:**
- Discard and Save become enabled after toolkit removal in a Toolkit Node
- Discard and Save become enabled after toolkit removal in an LLM Node
- Discard restores the toolkit
- Removal is not persisted without Save

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
| 2 | Open the Toolkit Node panel and click the X (clear) button next to the Toolkit field (Sharepoint). | Toolkit is removed from the node. **Save and Discard become enabled.** |
| 3 | Click Discard. | Toolkit Sharepoint, tool and Input Mapping are restored on the node and in TOOLS. Save and Discard are disabled. |
| 4 | Remove the toolkit again (X). Navigate away, choose Leave on the unsaved-changes prompt, then re-open the pipeline. | Pipeline loads with the toolkit still configured — the removal was not saved. |
| 5 | Open the pipeline with the LLM Node. Confirm Save and Discard are both disabled. | Save: disabled. Discard: disabled. |
| 6 | Open the LLM Node panel and remove the configured toolkit (Artifacts) from Toolkits & MCPs (X). | Toolkit entry is removed. Save and Discard become enabled. |
| 7 | Click Discard. | Artifacts toolkit is restored on the LLM Node. Save and Discard are disabled. |

## Expected Final State

Toolkit removal is tracked as an unsaved change in both node types and is fully reverted by Discard.

## Pass/Fail Criteria

**Pass:**
- Save and Discard become enabled after toolkit-only removal in both Toolkit Node and LLM Node
- Discard restores the removed toolkit
- Navigating away without saving does not persist the removal

**Fail:**
- Discard stays disabled after toolkit removal
- Discard does not restore the toolkit
- Removal is persisted without Save
