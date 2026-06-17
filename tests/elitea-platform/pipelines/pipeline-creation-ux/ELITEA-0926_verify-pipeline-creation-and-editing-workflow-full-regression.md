---
id: ELITEA-0926
title: "Verify Pipeline Creation and Editing Workflow — Full Regression"
priority: critical
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418]
requirements: [EliteaAI/elitea_issues#4418]
---
# ELITEA-0926: Verify Pipeline Creation and Editing Workflow — Full Regression

**Module:** Pipeline Creation Ux · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the end-to-end pipeline creation and editing workflow is fully functional after the pipeline UX refactor — including form, save, flow editor, YAML editor, and toolkit sections.

**Coverage:**
- End-to-end pipeline creation regression
- Flow editor functionality post-save
- YAML editor functionality post-save
- Toolkit section functionality post-save
- Edit existing pipeline — all sections accessible

## Preconditions

- Logged in
- Private project selected

## Test Data

- Pipeline Name: TC15-E2E-Regression-Pipeline
- Description: End to end regression test TC15

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Pipelines section | Pipelines list is displayed |
| 2 | Create a new pipeline: Name TC15-E2E-Regression-Pipeline, Description End to end regression test TC15, click Save | Pipeline is created and saved. Full edit form is displayed |
| 3 | Click on the Flow editor tab/section | Flow editor opens and is interactive |
| 4 | Add a node or connection in the Flow editor | Action is accepted without error |
| 5 | Click on the YAML editor tab/section | YAML editor opens and displays the pipeline YAML |
| 6 | Click on +Toolkit in the Toolkit section | Toolkit picker/dialog opens |
| 7 | Close the Toolkit picker without adding | Picker closes without error. Pipeline state is unchanged |
| 8 | Navigate back to Pipelines list, then re-open the pipeline for editing | Pipeline edit form opens with Flow, YAML, and Toolkit all active |
| 9 | Make a minor edit (e.g., update Welcome Message) and save | Edit saves without error |

## Expected Final State

Edit saves without error

## Pass/Fail Criteria

**Pass:**
- Full create-save-edit cycle completes without error
- Flow editor, YAML editor, and Toolkit section are all functional post-save
- Re-opening for edit keeps all sections active

**Fail:**
- Any stage of the create or edit flow fails
- Flow/YAML editor or Toolkit section is non-functional after save
