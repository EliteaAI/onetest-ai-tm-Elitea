---
id: ELITEA-3998
title: "Section Headers Clickable for Expand/Collapse"
priority: high
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-sections-redesign, usability, interaction]
requirements: [EL-6252]
---
# ELITEA-3998: Section Headers Clickable for Expand/Collapse

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking on section headers (Configuration, Tools, Indexes) toggles their expand/collapse state.

**Coverage:**
- Tools section header clickable to expand/collapse
- Indexes section header clickable to expand/collapse
- Configuration section header clickable (if collapsible)
- Entire header area is clickable, not just icon
- Visual feedback on click/hover

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
| 1 | Navigate to Toolkits & Indexes → open any toolkit. | Toolkit details page opens with default states. |
| 2 | Observe Tools section is collapsed by default. | Tools section collapsed, showing header with count. |
| 3 | Click on the "Tools" section header text/area. | Tools section expands showing all tools. |
| 4 | Observe expand/collapse indicator (arrow/chevron). | Indicator rotates or changes to show expanded state. |
| 5 | Click on the "Tools" section header again. | Tools section collapses. |
| 6 | Observe Indexes section is collapsed by default. | Indexes section collapsed. |
| 7 | Click on the "Indexes" section header. | Indexes section expands. |
| 8 | Click on the "Indexes" section header again. | Indexes section collapses. |
| 9 | Observe Configuration section state. | Configuration may be expandable/collapsible. |
| 10 | If Configuration has a header, click it to test expand/collapse. | Configuration toggles state (if applicable). |
| 11 | Hover over each section header. | Cursor changes to pointer indicating clickable area. |

## Expected Final State

All section headers respond to clicks by toggling expand/collapse state with appropriate visual feedback.

## Pass/Fail Criteria

**Pass:**
- Tools header click toggles expand/collapse
- Indexes header click toggles expand/collapse
- Configuration header responsive (if collapsible)
- Entire header area is clickable
- Visual feedback (cursor, indicator) on interaction

**Fail:**
- Header click doesn't toggle section
- Only icon/small area is clickable
- No visual feedback on hover/click
- Inconsistent behavior across sections
