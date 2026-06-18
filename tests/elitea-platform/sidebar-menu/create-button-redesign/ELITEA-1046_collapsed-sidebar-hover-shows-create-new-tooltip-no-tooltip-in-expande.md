---
id: ELITEA-1046
title: "Collapsed Sidebar: Hover Shows \"Create New\" Tooltip; No Tooltip in Expanded Mode"
priority: critical
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1046: Collapsed Sidebar: Hover Shows "Create New" Tooltip; No Tooltip in Expanded Mode

**Module:** Create Button Redesign · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that hovering over the `+` button in collapsed sidebar mode shows the universal "Create New" tooltip, and that no tooltip appears when the sidebar is expanded.

**Coverage:**
- Tooltip text accuracy in collapsed mode
- Tooltip absence in expanded mode

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Test performed in both collapsed and expanded sidebar states

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Collapse the sidebar; navigate to Agents | Sidebar is collapsed; `+` icon visible |
| 2 | Hover over the `+` icon | Tooltip appears with text "Create New" |
| 3 | Navigate to Pipelines (still collapsed); hover over `+` | Tooltip text is still "Create New" (not "Pipeline" or entity-specific) |
| 4 | Expand the sidebar; navigate to Agents | Sidebar is expanded; `+ Agent` button visible |
| 5 | Hover over the `+ Agent` button | No tooltip appears |

## Expected Final State

No tooltip appears

## Pass/Fail Criteria

**Pass:**
- Collapsed mode tooltip text is exactly \"Create New\" for every section
- No tooltip is shown in expanded mode

**Fail:**
- Tooltip shows an entity-specific name (e.g., \"Create Agent\") in collapsed mode
- Tooltip appears in expanded mode
- Tooltip text is empty or missing in collapsed mode
