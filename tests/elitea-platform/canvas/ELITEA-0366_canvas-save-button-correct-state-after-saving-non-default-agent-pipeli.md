---
id: ELITEA-0366
title: "Canvas Save Button — Correct State After Saving Non-Default Agent/Pipeline Version [Parametrized]"
priority: critical
type: functional
module: canvas
status: draft
execution_type: manual
tags: [eng:frontend, feat:canvas, ui]
requirements: [ProjectAlita/projectalita.github.io#3887]
---
# ELITEA-0366: Canvas Save Button — Correct State After Saving Non-Default Agent/Pipeline Version [Parametrized]

**Module:** Canvas · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after successfully saving a non-default (named, non-base) version in Canvas, the Save button is disabled, a second click without changes does not produce the error "Field required at version, author_id", and that making a subsequent change re-enables the Save button allowing a successful second save — all without closing Canvas.

**Coverage:**
- Save button transitions to disabled after a successful first save on a non-default version
- Second click on Save (no changes made) produces no API error and no UI error message
- New changes made after the first save re-enable the Save button without requiring Canvas to be reopened
- Second save after new changes completes successfully with no error
- Covers both Agent and Pipeline entity types

## Preconditions

- User is logged in at {{base_url}}
- A private or team project is open
- The project contains at least one Agent AND one Pipeline, each with a named non-default version created (not the base/default version)
- Browser DevTools Console is open to monitor network errors

## Test Data

| # | Entity Type | Version to Use |
|---|---|---|
| 1 | Agent | Any named non-base version (e.g., `v2`) |
| 2 | Pipeline | Any named non-base version (e.g., `v2`) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar. In the PARTICIPANTS section, add the target entity (Agent for row 1, Pipeline for row 2). | Entity is added as a participant in the Chat conversation. |
| 2 | In the version dropdown for the participant, select a non-default named version (not the base/default version). | The non-default version is selected and displayed in the participant card. |
| 3 | Click the pencil icon (Agent) or gear icon (Pipeline) to open Canvas. | Canvas panel opens for the selected non-default version. |
| 4 | Make a visible configuration change: for an Agent, edit at least one character of the System Prompt; for a Pipeline, change a step setting or model field. | The change is reflected in the Canvas editor. The Save button becomes active (enabled). |
| 5 | Click Save. | Save completes successfully. A success confirmation is shown or no error appears. The Save button becomes disabled (greyed out / not clickable). |
| 6 | Without making any further changes, attempt to click Save again. | The Save button is not clickable, OR if clicked, no API request is made and no error message appears in the UI. |
| 7 | Check the browser DevTools Console for any network errors or JS exceptions after step 6. | No 400 Bad Request or 'Field required at version, author_id' error in the console. |
| 8 | While still in Canvas (do NOT close or reopen it), make an additional configuration change (e.g., edit the System Prompt by one more character, or change another field). | The change is visible in the editor. The Save button becomes active (enabled) again — without needing to close and reopen Canvas. |
| 9 | Click Save. | The second save completes successfully. No 'Field required at version, author_id' or any other error is returned in the UI or in DevTools Console. |

## Expected Final State

The second save completes successfully. No 'Field required at version, author_id' or any other error is returned in the UI or in DevTools Console.

## Pass/Fail Criteria

**Pass:**
- First Save completes successfully for both Agent (row 1) and Pipeline (row 2)
- Save button is disabled immediately after the first successful save
- Second click on Save (without changes) produces no error and makes no API call
- Making a new change re-enables Save button without closing Canvas
- Second Save completes successfully with no error for both entity types

**Fail:**
- Save button remains clickable/active after a successful first save
- Second click on Save returns "Field required at version, author_id" or any other error message
- Save button does not re-enable after a new change is made (Canvas must be closed/reopened to restore button)
- Any of the above behaviors occur for either entity type (Agent or Pipeline)
