---
id: ELITEA-0264
title: "Configured Tab: List/Grid Toggle"
priority: high
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770]
---
# ELITEA-0264: Configured Tab: List/Grid Toggle

**Module:** Applications · **Priority:** High · **Type:** Functional

**Objective:** Verify that switching between grid and list views works correctly and renders the correct columns.

**Coverage:**
- Toggle icons visible in top-right
- List view columns: Name & Description, Authors, Created, Actions
- Description on second line, truncated author names, date format, three-dot menu
- Switching back to grid restores card layout

## Preconditions

- Logged in as a project member
- On the Configured tab with multiple apps listed (including apps with descriptions and from different authors)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | On the Configured tab, locate the grid/list toggle icons in the top-right corner | Both grid and list toggle icons are visible |
| 2 | Click the List view icon | Table renders with columns: Name & Description, Authors, Created, Actions |
| 3 | Observe the Name & Description column for an app that has a description | Description appears on a second line below the name |
| 4 | Observe the Authors column | Author avatar and truncated name (e.g., 'Marian…') are shown |
| 5 | Observe the Created column | Abbreviated date format (e.g., 'May, 18') is shown |
| 6 | Observe the Actions column | Three-dot (⋮) context menu icon appears per row |
| 7 | Click the Grid view icon | Card layout is restored correctly |

## Expected Final State

Card layout is restored correctly

## Pass/Fail Criteria

**Pass:**
- All columns render correctly in list view
- Grid is restored on toggle back

**Fail:**
- Columns missing or incorrect, or grid not restored after toggling back
