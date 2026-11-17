---
id: ELITEA-0915
title: "Verify Save Is Blocked When the Required Name Field Is Empty"
priority: critical
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418, epic:7093]
requirements: [EliteaAI/elitea_issues#4418, EliteaAI/elitea_issues#7154]
---
# ELITEA-0915: Verify Save Is Blocked When the Required Name Field Is Empty

> **Updated for Pipelines 2.0:** Creation is canvas-first (#7154) and only Name is required. Description is optional, so the Description-empty scenario now saves successfully.

**Module:** Pipeline Creation Ux · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Save is blocked with visible validation feedback when the required Name field is empty, and that an empty Description does not block saving.

**Coverage:**
- Validation when Name is empty
- Validation when Name contains only whitespace
- Description is optional (empty Description saves)
- Save button state under each condition

## Preconditions

- Logged in
- Private project selected

## Test Data

| Scenario | Name | Description |
|---|---|---|
| Name empty | (empty) | Some description |
| Name whitespace only | `   ` | (empty) |
| Description empty | TC4-Test-Pipeline | (empty) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click **+ Pipeline** to create a new pipeline | The new pipeline opens directly on the canvas (empty-state card *"Start by adding your first node to the canvas!"*). Name is pre-filled (e.g. "Pipeline N") |
| 2 | Clear the Name field. Enter Description "Some description". Click Save | Save is blocked. A validation error is shown on the Name field |
| 3 | Enter only spaces in Name. Click Save | Save is blocked. Whitespace-only Name is treated as empty |
| 4 | Enter Name "TC4-Test-Pipeline", leave Description empty. Click Save | Pipeline is saved successfully. No validation error for Description |

## Expected Final State

The pipeline "TC4-Test-Pipeline" is saved with an empty Description.

## Pass/Fail Criteria

**Pass:**
- Save is blocked when Name is empty or whitespace-only
- Visible validation feedback is shown on the Name field
- Save succeeds with a valid Name and an empty Description

**Fail:**
- Save proceeds with an empty or whitespace-only Name
- No validation feedback is shown for an empty Name
- Save is blocked because Description is empty
