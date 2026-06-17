---
id: ELITEA-0101
title: "Tool Card Height Increase Does Not Clip Controls or Break Card Layout"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3833]
---
# ELITEA-0101: Tool Card Height Increase Does Not Clip Controls or Break Card Layout

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the increased Tool Card height correctly accommodates the variables toggle row without clipping any card content, overflowing adjacent cards, or breaking the TOOLKITS section layout.

**Coverage:**
- Cards for nested agents with variables are visibly taller than cards for plain toolkits
- No card content (name, show/hide tools icon, delete button, open-in-new-tab button) is clipped or hidden due to the height change
- Cards without variables are unaffected in height
- TOOLKITS section layout remains aligned and scrollable with mixed card heights
- No `overflow: hidden` clips the variables toggle row

## Preconditions

- Logged in to elitea.ai with
- Private project context selected
- A **parent Agent** exists that has **at least two entries in TOOLKITS**:
  1. A **nested child Agent** that has ≥ 1 variable defined (so the "Show variables (N)" toggle appears)
  2. A **plain toolkit** (e.g., Artifacts) that has no variables — producing a Tool Card without the toggle
- Browser: Chromium-based, desktop, DevTools available

## Test Data

| Item | Value |
|---|---|
| Variable-bearing card | Nested child Agent with `{{var1}}` defined |
| Non-variable card | Artifacts toolkit |
| Viewport widths | 768 px, 1024 px, 1280 px |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the parent Agent's detail page. Open the TOOLKITS section. | Both Tool Cards are visible: one for the nested child Agent (with variables) and one for the plain Artifacts toolkit (without variables). |
| 2 | Visually compare the height of the variable-bearing card (nested agent) against the non-variable card (Artifacts toolkit). | The variable-bearing card is measurably taller, accommodating the 'Show variables (N)' toggle row. The Artifacts card height is unchanged. |
| 3 | On the variable-bearing card, verify all standard controls are fully visible and not clipped: toolkit name, 'Show tools / Hide tools' toggle, open-in-new-tab button, and delete button. | All controls are fully visible and not partially hidden or overlapping each other. |
| 4 | Open DevTools → Inspect the variable-bearing card container. Check CSS for any `overflow: hidden` that would clip the variables toggle row. | The variables toggle row is not subject to a clipping overflow rule — the row is fully within the rendered card bounds. |
| 5 | Scroll through the full TOOLKITS section. | All cards remain vertically aligned. No card overlaps another. No broken layout. |
| 6 | Set browser viewport to 768 px and repeat the height and layout checks. | Card heights and layout remain correct at narrow viewport — no regression from combining height change with narrow layout. |

## Expected Final State

Card heights and layout remain correct at narrow viewport — no regression from combining height change with narrow layout.

## Pass/Fail Criteria

**Pass:**
- Variable-bearing nested agent cards are taller than plain toolkit cards
- All card controls are fully visible and not clipped
- No overflow clipping of the variables toggle row
- TOOLKITS section layout is consistent and scrollable

**Fail:**
- Any card control is clipped, hidden, or overlapping due to the height change
- Nested agent card with variables has the same height as a plain toolkit card
- Cards overlap or misalign in the TOOLKITS section
- DevTools shows the toggle row is clipped by overflow:hidden
