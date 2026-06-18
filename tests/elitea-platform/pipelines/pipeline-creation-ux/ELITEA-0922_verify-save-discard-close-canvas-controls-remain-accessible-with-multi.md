---
id: ELITEA-0922
title: "Verify Save/Discard/Close Canvas Controls Remain Accessible With Multiple Conversation Starters"
priority: high
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418, 4685]
requirements: [EliteaAI/elitea_issues#4418, EliteaAI/elitea_issues#4685]
---
# ELITEA-0922: Verify Save/Discard/Close Canvas Controls Remain Accessible With Multiple Conversation Starters

**Module:** Pipeline Creation Ux · **Priority:** High · **Type:** Functional

**Objective:** Verify that Save, Discard Changes, and Close Canvas buttons remain accessible and functional regardless of how many conversation starters have been added (up to the maximum of 4).

**Coverage:**
- Accessibility of action controls with 1–4 conversation starters
- User ability to save or discard without needing to refresh

## Preconditions

- Logged in
- Private project selected
- Chat pipeline participant configuration panel is open

## Test Data

- 4 conversation starters: Starter 1, Starter 2, Starter 3, Starter 4

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline participant configuration panel in Chat | Panel is displayed. Save, Discard/Cancel, and Close/X buttons are visible |
| 2 | Add all 4 conversation starters | All 4 starters are added |
| 3 | Scroll to the bottom of the configuration page | Bottom of the page is reached |
| 4 | Scroll back to the top of the page | Top of the page is reached |
| 5 | Verify Save button is visible and clickable | Save button is accessible |
| 6 | Verify Discard/Cancel button is visible and clickable | Discard/Cancel button is accessible |
| 7 | Verify Close/X button of the canvas is visible and clickable | Close button is accessible |
| 8 | Click Save | Pipeline participant is saved without error |

## Expected Final State

Pipeline participant is saved without error

## Pass/Fail Criteria

**Pass:**
- Save, Discard, and Close buttons remain accessible after adding 4 conversation starters
- User can save or discard without needing to refresh the page

**Fail:**
- Any action button becomes inaccessible after adding conversation starters
- User is forced to refresh the page to access Save/Discard/Close
