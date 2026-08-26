---
id: ELITEA-2820
title: "Section Expand/Collapse State Preserved During Session"
priority: high
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-sections-redesign, state-management, usability]
requirements: [EL-6252]
---
# ELITEA-2820: Section Expand/Collapse State Preserved During Session

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify that manually set expand/collapse states for sections are preserved while the user remains on the page.

**Coverage:**
- Manually expanded sections stay expanded
- Manually collapsed sections stay collapsed
- State preserved when switching between Form and Raw JSON views
- State preserved during other interactions on the page

## Preconditions

- Logged in to {{base_url}}
- A toolkit with Configuration, Tools, and Indexes sections

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any existing toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → open any toolkit. | Toolkit details page opens with default states (Config expanded, Tools collapsed). |
| 2 | Expand the Tools section by clicking its header. | Tools section expands. |
| 3 | Note the current state: Configuration expanded, Tools expanded. | States recorded. |
| 4 | Switch to Raw JSON view using the icon control. | View changes to Raw JSON editor. |
| 5 | Switch back to Form view. | View returns to Form view. |
| 6 | Observe section states. | Configuration still expanded, Tools still expanded. |
| 7 | Click "Show more" then "Show less" in Configuration. | Toggle occurs. |
| 8 | Observe Tools section state. | Tools section remains expanded. |
| 9 | Modify a field value (without saving). | Field modified. |
| 10 | Observe all section states. | All manually set expand/collapse states preserved. |

## Expected Final State

All sections retain their manually set expand/collapse states throughout interactions on the page.

## Pass/Fail Criteria

**Pass:**
- Expanded sections stay expanded during view switches
- Collapsed sections stay collapsed
- State preserved across all page interactions
- No unexpected state resets

**Fail:**
- Sections reset to default state on view switch
- Manually set state lost during interactions
- Random state changes
