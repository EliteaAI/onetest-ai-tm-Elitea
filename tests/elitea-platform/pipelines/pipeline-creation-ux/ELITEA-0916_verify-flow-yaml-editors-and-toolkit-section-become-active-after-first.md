---
id: ELITEA-0916
title: "Verify Flow/YAML Editors and Toolkit Section Become Active After First Save"
priority: critical
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418]
requirements: [EliteaAI/elitea_issues#4418]
---
# ELITEA-0916: Verify Flow/YAML Editors and Toolkit Section Become Active After First Save

**Module:** Pipeline Creation Ux · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that on successful first save, the pipeline detail view immediately enables the Flow editor, YAML editor, and Toolkit add buttons all in a single state transition.

**Coverage:**
- State transition of the full pipeline edit form after initial save
- Concurrent activation of Flow editor, YAML editor, and Toolkit section

## Preconditions

- Logged in
- Private project selected
- New pipeline creation form is open with only basic fields visible

## Test Data

- Pipeline Name: TC5-PostSave-Pipeline
- Description: Test description TC5

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Create New Pipeline form | Form is displayed |
| 2 | Enter Name (TC5-PostSave-Pipeline) and Description (Test description TC5) | Fields are populated |
| 3 | Click Save | Save succeeds. Success confirmation displayed. Pipeline detail view is shown |
| 4 | Verify the Flow editor tab/section is now active | Flow editor is accessible and interactive |
| 5 | Verify the YAML editor tab/section is now active | YAML editor is accessible and interactive |
| 6 | Verify the +Toolkit, +MCP, +Agent, +Pipeline buttons in the Toolkit section are active | All four add buttons are clickable |
| 7 | Attempt to add a node in the Flow editor | Flow editor accepts the action without error |
| 8 | Attempt to switch to YAML editor | YAML view is rendered without error |

## Expected Final State

YAML view is rendered without error

## Pass/Fail Criteria

**Pass:**
- All three sections (Flow, YAML, Toolkit) transition to active state immediately after first save
- Interactions with Flow editor, YAML editor, and Toolkit add buttons all work without errors

**Fail:**
- Any section remains inactive/disabled after successful save
- Errors occur when attempting to interact with the newly activated sections
