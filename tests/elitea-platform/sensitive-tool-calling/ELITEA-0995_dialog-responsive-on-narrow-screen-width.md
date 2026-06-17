---
id: ELITEA-0995
title: "Dialog Responsive on Narrow Screen Width"
priority: medium
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-0995: Dialog Responsive on Narrow Screen Width

**Module:** Sensitive Tool Calling · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the authorization dialog remains usable and does not overflow horizontally when the browser window is set to a narrow width (~400px).

## Preconditions

- Browser window can be resized

## Test Data

- Target viewport width: 400px

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Resize the browser window to approximately 400px width. | Page adjusts to narrow layout. |
| 2 | Trigger a sensitive tool so the authorization dialog appears. | Authorization dialog appears within the viewport. |
| 3 | Observe the dialog layout. | Dialog is contained within the visible area. No horizontal page overflow. Buttons may stack vertically if needed. |
| 4 | Verify both [Authorize] and [Block] buttons are visible and clickable at 400px width. | Both buttons are accessible and clickable without scrolling horizontally. |
| 5 | Click [Block] to dismiss the dialog. | Dialog closes. Layout returns to normal. |

## Expected Final State

Dialog closes. Layout returns to normal.

## Pass/Fail Criteria

Pass:
- Dialog fits within the 400px viewport
- Buttons are accessible (no need for horizontal scrolling to reach them)
- No horizontal overflow on the page

Fail:
- Dialog extends beyond viewport at 400px
- Buttons are cut off or unreachable at narrow width
