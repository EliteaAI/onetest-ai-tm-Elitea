---
id: ELITEA-0915
title: "Verify Save Is Blocked When Required Fields Are Empty"
priority: critical
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418]
requirements: [EliteaAI/elitea_issues#4418]
---
# ELITEA-0915: Verify Save Is Blocked When Required Fields Are Empty

**Module:** Pipeline Creation Ux · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Save button is blocked and appropriate validation feedback is shown when Name or Description fields are empty.

**Coverage:**
- Validation when Name is empty
- Validation when Description is empty
- Validation when both Name and Description are empty
- Save button state under each condition

## Preconditions

- Logged in
- Private project selected
- New pipeline creation form opened

## Test Data

Scenario | Name | Description
Both empty | (empty) | (empty)
Name empty only | (empty) | Some description
Description empty only | TC4-Test-Pipeline | (empty)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Create New Pipeline form | Form is displayed |
| 2 | Leave both Name and Description empty. Click Save | Save is blocked. Validation error(s) shown indicating required fields are missing |
| 3 | Enter only Description (Some description), leave Name empty. Click Save | Save is blocked. Validation error shown on Name field |
| 4 | Clear Description. Enter only Name (TC4-Test-Pipeline), leave Description empty. Click Save | Save is blocked. Validation error shown on Description field |
| 5 | Enter valid Name (TC4-Test-Pipeline) and valid Description (Test description TC4). Click Save | Pipeline is saved successfully. No validation errors shown |

## Expected Final State

Pipeline is saved successfully. No validation errors shown

## Pass/Fail Criteria

**Pass:**
- Save is blocked in all three missing-field scenarios
- Visible validation feedback is shown for each missing required field
- Save succeeds when both Name and Description are provided

**Fail:**
- Save proceeds with empty Name or Description
- No validation feedback is shown for missing required fields
