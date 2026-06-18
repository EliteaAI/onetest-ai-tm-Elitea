---
id: ELITEA-0795
title: "LLM Node — Toolkit Entry and Tools Section Are Removed After Toolkit Is Removed"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5105]
---
# ELITEA-0795: LLM Node — Toolkit Entry and Tools Section Are Removed After Toolkit Is Removed

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that removing a toolkit from the Toolkits section of an LLM Node removes both the toolkit entry and its associated Tools sub-section completely.

**Coverage:**
- Toolkit entry (e.g., `Artifacts toolkit (0/0)`) is removed from the LLM Node Toolkits section
- The Tools sub-section associated with the removed toolkit disappears
- No toolkit name, tool count badge, or Tools panel remains
- Saved and reloaded state is clean

## Preconditions

- Logged in to {{base_url}}
- A pipeline is saved with an LLM Node that has at least one toolkit attached in the Toolkits section (e.g., Artifacts toolkit or Artifactregression)
- Save and Discard buttons are disabled before starting

## Test Data

- Pipeline: "Discarding changes bug" (or equivalent)
- LLM Node toolkit: Artifacts / Artifactregression
- Expected toolkit entry label: Artifactregression (0/0)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline in edit mode. Locate the LLM Node and expand the Toolkits section. | LLM Node is visible. The Toolkits section shows at least one toolkit entry (e.g., Artifactregression (0/0)) with a Tools sub-section inside. |
| 2 | Click the × / remove button next to the toolkit entry (e.g., Artifactregression) in the Toolkits section. | The toolkit entry disappears from the Toolkits section. |
| 3 | Observe the Toolkits section. | The entire toolkit block — including the toolkit name, the tool count badge, and the Tools sub-section — is gone. The Toolkits section is empty or shows only the add-toolkit controls. |
| 4 | Observe the Save and Discard button states. | Save remains inactive. Toolkit removal is auto-saved to the backend immediately — no manual Save is needed. |
| 5 | Reload the pipeline and inspect the LLM Node Toolkits section. | The LLM Node Toolkits section is empty. No toolkit entry, badge, or Tools section is present. |

## Expected Final State

The LLM Node Toolkits section is empty. No toolkit entry, badge, or Tools section is present.

## Pass/Fail Criteria

**Pass:**
- The toolkit entry and its Tools sub-section are fully removed after clicking remove
- Save button remains inactive after removal (auto-saved immediately)
- Reloaded pipeline shows a clean LLM Node Toolkits section

**Fail:**
- The toolkit entry (name or badge) remains in the LLM Node after removal
- The Tools sub-section remains visible even though the toolkit was removed
- Save button unexpectedly becomes active after toolkit removal
- Reload causes the toolkit entry to reappear
