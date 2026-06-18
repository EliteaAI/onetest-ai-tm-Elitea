---
id: ELITEA-0217
title: "Creativity Slider Adjustable and Saved on Apply in Model Settings"
priority: high
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0217: Creativity Slider Adjustable and Saved on Apply in Model Settings

**Module:** Agents Studio · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Creativity slider in the Model Settings dialog is interactive and its value is saved when Apply is clicked.

**Coverage:**
- Creativity slider can be moved to any value (1–5)
- Apply persists the selected value for the session

## Preconditions

- Published agent is open in chat
- Model Settings dialog is accessible

## Test Data

Creativity value: 3 (change from default 1 or 2)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Model Settings dialog via the gear icon. | Dialog opens with Creativity slider. |
| 2 | Move the Creativity slider to position 3. | Slider moves to position 3. |
| 3 | Click Apply. | Dialog closes without error. |
| 4 | Reopen Model Settings dialog. | Creativity slider shows value 3. |

## Expected Final State

Creativity slider shows value 3.

## Pass/Fail Criteria

**Pass:**
- Slider is draggable across the full 1–5 range
- Value 3 is retained after Apply and visible on dialog reopen

**Fail:**
- Slider is not interactive
- Value resets to default after Apply
