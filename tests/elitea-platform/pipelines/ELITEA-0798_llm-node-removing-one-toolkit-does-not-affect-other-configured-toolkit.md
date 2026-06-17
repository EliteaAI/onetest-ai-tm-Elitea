---
id: ELITEA-0798
title: "LLM Node — Removing One Toolkit Does Not Affect Other Configured Toolkits"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5105]
---
# ELITEA-0798: LLM Node — Removing One Toolkit Does Not Affect Other Configured Toolkits

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that when an LLM Node has multiple toolkits configured and one is removed, the remaining toolkits and their Tools sections are unaffected and retain their configuration.

**Coverage:**
- Removed toolkit entry disappears from LLM Node
- Remaining toolkit entries are intact with their name, badge, and Tools sub-sections
- Enabled tools in the remaining toolkits retain their enabled state
- Saved and reloaded state is correct for the remaining toolkits

## Preconditions

- Logged in to {{base_url}}
- A pipeline saved with an LLM Node that has at least two toolkits in the Toolkits section (e.g., Artifacts and Sharepoint) with at least one tool enabled per toolkit

## Test Data

- Toolkit to keep: Artifacts (with ≥1 tool enabled)
- Toolkit to remove: Sharepoint

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline in edit mode. Expand the LLM Node Toolkits section. | At least two toolkit entries are visible (Artifacts and Sharepoint). Each has a Tools sub-section. |
| 2 | Remove the Sharepoint toolkit by clicking its × / remove button. | The Sharepoint toolkit entry and its Tools sub-section disappear from the LLM Node. |
| 3 | Observe the Artifacts toolkit entry. | The Artifacts entry remains visible with its name, badge, and Tools sub-section intact. Previously enabled tools are still enabled. |
| 4 | Click Save. | Pipeline is saved. |
| 5 | Reload the pipeline and inspect the LLM Node Toolkits section. | Only Artifacts toolkit is present. Sharepoint is absent. The Artifacts entry retains its correct tool configuration. |

## Expected Final State

Only Artifacts toolkit is present. Sharepoint is absent. The Artifacts entry retains its correct tool configuration.

## Pass/Fail Criteria

**Pass:**
- Only the removed toolkit disappears; all other toolkit entries are unchanged
- Enabled tools in remaining toolkits are unaffected
- Post-save reload confirms correct state

**Fail:**
- Removing one toolkit also removes or corrupts another toolkit's entry or tools
- The remaining toolkit's tool count or enabled tools change unexpectedly after removal of a different toolkit
