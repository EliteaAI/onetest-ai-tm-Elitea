---
id: ELITEA-0792
title: "Toolkit Node — Input Mapping Populates Correctly When Adding a Toolkit and Tool"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5105]
---
# ELITEA-0792: Toolkit Node — Input Mapping Populates Correctly When Adding a Toolkit and Tool

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that selecting a toolkit and then a tool in a Toolkit Node correctly populates the Input Mapping section with the tool's expected parameter fields, and that saving retains the configuration.

**Coverage:**
- Selecting a toolkit enables the Tool dropdown
- Selecting a tool populates the Input Mapping section with tool-specific fields
- Input Mapping values can be entered and saved
- Reload retains the toolkit, tool, and Input Mapping values

## Preconditions

- Logged in to {{base_url}}
- A pipeline exists with a Toolkit Node that has no toolkit selected (empty state)
- Access to at least one configured toolkit (e.g., Sharepoint) in the project

## Test Data

- Toolkit: Sharepoint
- Tool: remove_index
- Input Mapping field: Index name
- Input Mapping value: test-index

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a pipeline in edit mode. Locate the Toolkit Node with no toolkit selected. | Toolkit Node shows empty Toolkit and Tool dropdowns. Input Mapping section is absent or empty. |
| 2 | Click the Toolkit dropdown and select Sharepoint. | Sharepoint is selected. Tool dropdown becomes available. |
| 3 | Click the Tool dropdown and select remove_index. | remove_index is selected. |
| 4 | Observe the Input Mapping section. | The Input Mapping section appears and contains the expected field: Index name (and any other fields defined for remove_index). |
| 5 | Enter 'test-index' in the Index name field (using Fixed type). | Value is accepted. |
| 6 | Click Save. | Pipeline is saved. |
| 7 | Reload the pipeline and inspect the Toolkit Node. | Toolkit Node shows: Toolkit = Sharepoint, Tool = remove_index, Input Mapping section present with Index name = test-index. |

## Expected Final State

Toolkit Node shows: Toolkit = Sharepoint, Tool = remove_index, Input Mapping section present with Index name = test-index.

## Pass/Fail Criteria

**Pass:**
- Input Mapping section appears and displays correct tool-specific fields after tool selection
- Values are retained after save and reload

**Fail:**
- Input Mapping section does not appear after selecting the tool
- Input Mapping fields are incorrect, missing, or from a different tool
- Values are lost after save/reload
