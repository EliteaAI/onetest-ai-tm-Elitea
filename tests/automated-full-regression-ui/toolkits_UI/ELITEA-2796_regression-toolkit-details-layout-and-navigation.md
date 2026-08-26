---
id: ELITEA-2796
title: "Regression - Toolkit Details Layout and Navigation"
priority: critical
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, smoke, toolkit-redesign, layout]
requirements: []
---
# ELITEA-2796: Regression - Toolkit Details Layout and Navigation

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Regression / Smoke

**Objective:** Verify toolkit details page displays correctly with two-column layout and all navigation paths work after redesign.

**Coverage:**
- Two-column layout (config/tools left, indexes right)
- Toolkit list to details navigation
- Index card to Index Details navigation
- Breadcrumb navigation at all levels
- Save/Discard functionality

## Preconditions

- Logged in to {{base_url}} with edit permissions
- At least one toolkit with indexes exists

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any existing toolkit with at least one index |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes list page. | List displays all toolkits. |
| 2 | Click on any toolkit. | Details page opens with two-column layout: left (config, tools), right (indexes). |
| 3 | Verify left panel contents. | Name, Description, Credentials, Show more link, Form/Raw JSON toggle, TOOLS section with count visible. |
| 4 | Verify right panel contents. | "Indexes (N)" header, index cards or empty state. |
| 5 | Modify Description and click Discard. | Changes revert to original. |
| 6 | Modify Description and click Save. | Changes persist; refresh confirms save. |
| 7 | Click an index card. | Index Details page opens; breadcrumb shows full path. |
| 8 | Click "Search" button. | Search page opens; breadcrumb includes "Search". |
| 9 | Click toolkit name in breadcrumb. | Returns to Toolkit Details page. |
| 10 | Click "Toolkits & Indexes" in breadcrumb. | Returns to list page. |

## Expected Final State

All navigation paths work correctly, and page layouts display as designed.

## Pass/Fail Criteria

**Pass:**
- Layout renders correctly
- All navigation paths work
- Save/Discard functions properly
- Breadcrumbs navigate accurately

**Fail:**
- Broken layout
- Navigation failures
- Save/Discard broken
- Incorrect breadcrumbs
