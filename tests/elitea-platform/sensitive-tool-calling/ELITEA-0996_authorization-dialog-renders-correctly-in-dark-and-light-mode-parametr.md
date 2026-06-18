---
id: ELITEA-0996
title: "Authorization Dialog Renders Correctly in Dark and Light Mode [Parametrized]"
priority: medium
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-0996: Authorization Dialog Renders Correctly in Dark and Light Mode [Parametrized]

**Module:** Sensitive Tool Calling · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the authorization dialog renders with correct contrast, readable text, and proper button styling in both Dark mode and Light mode themes. [Parametrized]

## Preconditions

- The ELITEA platform supports switching between Dark and Light mode

## Test Data

Theme modes to test: Dark mode, Light mode

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Switch the ELITEA platform to Dark mode. | Theme switch applied. |
| 2 | Trigger a sensitive tool so the authorization dialog appears. | Dialog appears. |
| 3 | Observe the dialog background, text color, and contrast in Dark mode. | Text is legible. Background and text have sufficient contrast for Dark mode. |
| 4 | Observe the Authorize and Block buttons in Dark mode. | Both buttons are visible with proper styling (not blending into background). |
| 5 | Observe the warning border on the dialog in Dark mode. | Amber/warning border is visible in Dark mode. |
| 6 | Switch the platform to Light mode. Trigger the dialog again. | Theme switch applied. Dialog appears. |
| 7 | Observe dialog background, text color, contrast, buttons, and warning border in Light mode. | All elements are legible and properly styled. Warning border is visible in Light mode. |

## Expected Final State

All elements are legible and properly styled. Warning border is visible in Light mode.

## Pass/Fail Criteria

Pass:
- Dialog is legible and properly styled in both Dark and Light modes
- Buttons are clearly visible in both themes
- Warning border is visible in both themes

Fail:
- Text or buttons become invisible due to contrast failures in either mode
- Warning border is indistinguishable in either mode
