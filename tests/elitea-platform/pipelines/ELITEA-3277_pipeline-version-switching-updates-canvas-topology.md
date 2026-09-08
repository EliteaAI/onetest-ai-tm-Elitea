---
id: ELITEA-3277
title: "Pipeline version switching updates canvas topology correctly"
priority: critical
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:pipelines, feat:version-selector, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor/Admin role
- Private project context is selected
- Pipeline exists with at least 2 versions having different canvas topologies (different nodes/connections)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Pipeline | Pipeline with "v1" (3 nodes, 2 connections) and "v2" (5 nodes, 4 connections) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Pipeline with multiple versions | Pipeline loads with current version |
| 2 | Note the current version name displayed in the selector | Version name is visible (e.g., "v1") |
| 3 | Note the current canvas topology (number of nodes, connections, layout) | Canvas shows v1 topology (3 nodes, 2 connections) |
| 4 | Open the version selector dropdown | Dropdown opens with version list |
| 5 | Select a different version (e.g., "v2") | Version switches |
| 6 | Verify the version selector now displays the new version name | Selector shows "v2" |
| 7 | Verify the canvas topology updates to match the selected version | Canvas shows v2 topology (5 nodes, 4 connections) |
| 8 | Verify all nodes are rendered correctly | Nodes display with correct labels and configurations |
| 9 | Verify all connections are rendered correctly | Connections match v2 configuration |
| 10 | Switch back to the first version | First version loads |
| 11 | Verify canvas reverts to the original topology | Canvas matches v1 topology again |

## Expected Final State

Version selector displays the selected version name, and the canvas topology updates to accurately reflect the selected version's configuration.

## Pass/Fail Criteria

**Pass:**
- Version selector updates to show selected version name
- Canvas topology updates to match selected version
- All nodes and connections render correctly
- Switching back and forth works consistently
- No visual glitches or errors during transition

**Fail:**
- Version selector doesn't update to new version name
- Canvas topology doesn't update or shows incorrect configuration
- Nodes or connections are missing or incorrect
- Errors occur during version switching
- Canvas displays outdated or mixed version state
