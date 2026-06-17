---
id: ELITEA-0964
title: "Responsive Layout: Cards Stack Vertically at Narrow Window Widths"
priority: medium
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0964: Responsive Layout: Cards Stack Vertically at Narrow Window Widths

**Module:** Resources · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the 4 resource cards transition from a 2-column grid to a single-column vertical stack when the browser window is narrowed, without any overlap, clipping, or horizontal scrollbar.

**Coverage:**
- 2×2 grid at full width (1440px)
- Layout reflow at 1024px, 768px, 480px
- Single-column stack at narrow widths
- Restoration of 2-column layout on window expand

## Preconditions

Logged in to ELITEA; on the Resources page
Browser window resizable (Chrome/Firefox DevTools or manual drag)

## Test Data

Test widths: 1440px (full), 1024px, 768px, 480px (narrow)
Expected layout: 2×2 grid at full width; single column at narrow widths

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Resources page in a full-width browser window (~1440px). | Cards are displayed in a 2×2 grid layout. |
| 2 | Resize the browser window to ~1024px wide. | Cards resize proportionally; no overlap or clipping; no unexpected horizontal scrollbar. |
| 3 | Resize the browser window to ~768px wide. | Cards continue to resize; layout may begin to reflow to single column; no overlap or clipping. |
| 4 | Resize the browser window to ~480px wide. | Cards are stacked vertically in a single column; all card content is visible and legible. |
| 5 | Confirm no card text or content overflows outside the card boundary at 480px. | All card content contained within card boundaries. |
| 6 | Expand the window back to full width (~1440px). | The 2×2 grid layout is fully restored. |

## Expected Final State

The 2×2 grid layout is fully restored.

## Pass/Fail Criteria

**Pass:**
- Cards display in 2×2 grid at 1440px
- Cards reflow and stack vertically before content clips or overlaps
- No card text or content overflows outside card boundary at any tested width
- No cards overlap each other at any intermediate width
- 2-column layout restored when window expanded back to full width

**Fail:**
- Cards overlap at any tested width
- Card content clips outside the card boundary
- Horizontal scrollbar appears unexpectedly
- 2-column layout not restored after window expansion
