---
id: ELITEA-0218
title: "Cancel and X Button Discard Changes in Model Settings Dialog"
priority: high
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0218: Cancel and X Button Discard Changes in Model Settings Dialog

**Module:** Agents Studio · **Priority:** High · **Type:** Functional

**Objective:** Verify that both the Cancel button and the X (close) button dismiss the Model Settings dialog without saving any changes.

**Coverage:**
- Cancel discards unsaved changes
- X close button behaves identically to Cancel

## Preconditions

- Published agent is open in chat, previously applied settings are known

## Test Data

Change Creativity to 5, do NOT click Apply

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Model Settings dialog. Note the current Creativity value (e.g. 1). | Dialog open, Creativity = 1. |
| 2 | Move Creativity slider to 5. | Slider shows 5. |
| 3 | Click Cancel. | Dialog closes. |
| 4 | Reopen dialog. | Creativity still shows 1 (unchanged). |
| 5 | Repeat steps 1–2 (set Creativity to 5). | Slider shows 5. |
| 6 | Click the × close button in the top-right of the dialog. | Dialog closes. |
| 7 | Reopen dialog. | Creativity still shows 1. |

## Expected Final State

Creativity still shows 1.

## Pass/Fail Criteria

**Pass:**
- Both Cancel and × close revert to prior values without saving
- No change is applied after either action

**Fail:**
- Slider value 5 is saved after Cancel or × close
- Settings dialog applies changes without an explicit Apply action
