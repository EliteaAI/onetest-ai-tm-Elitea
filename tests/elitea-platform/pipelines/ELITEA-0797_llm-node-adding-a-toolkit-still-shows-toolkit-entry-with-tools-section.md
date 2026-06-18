---
id: ELITEA-0797
title: "LLM Node — Adding a Toolkit Still Shows Toolkit Entry with Tools Section Correctly"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5105]
---
# ELITEA-0797: LLM Node — Adding a Toolkit Still Shows Toolkit Entry with Tools Section Correctly

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that after the fix, adding a toolkit to an LLM Node correctly displays the toolkit entry, its tool count, and the Tools sub-section with selectable tools.

**Coverage:**
- Toolkit entry appears in the LLM Node Toolkits section after adding
- Toolkit name and count badge (e.g., Artifacts toolkit (0/0)) are displayed
- Tools sub-section is visible and contains tool options
- Enabling tools updates the tool count badge
- Configuration is retained after Save and reload

## Preconditions

- Logged in to {{base_url}}
- A pipeline with an LLM Node that currently has no toolkits attached
- Access to at least one toolkit in the project (e.g., Artifacts)

## Test Data

- LLM Node: LLM 1
- Toolkit to add: Artifacts (or Artifactregression)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a pipeline in edit mode. Locate an LLM Node with no toolkits. Expand the Toolkits section. | Toolkits section is visible and empty. Toolkit/MCP/Agent/Pipeline add buttons are visible. |
| 2 | Click the Toolkit add button in the Toolkits section. | A toolkit selector dropdown appears. |
| 3 | Select the Artifacts toolkit from the dropdown. | The toolkit entry 'Artifacts toolkit (0/0)' appears in the Toolkits section. |
| 4 | Expand the toolkit entry. | The Tools sub-section is visible with a list of available tools with checkboxes or toggles. |
| 5 | Enable at least one tool. | The tool count in the badge updates (e.g., Artifacts toolkit (1/N)). |
| 6 | Click Save. | Pipeline is saved. |
| 7 | Reload the pipeline. Inspect the LLM Node Toolkits section. | Toolkit entry is present with the correct name and updated tool count. Enabled tools remain enabled. |

## Expected Final State

Toolkit entry is present with the correct name and updated tool count. Enabled tools remain enabled.

## Pass/Fail Criteria

**Pass:**
- Toolkit entry with name and count badge is shown after adding
- Tools sub-section is present and functional
- Configuration persists after save/reload

**Fail:**
- Toolkit entry does not appear after adding
- Tools sub-section is missing or empty when it should have tool options
- Count badge does not update when tools are enabled
