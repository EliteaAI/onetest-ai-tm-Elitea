---
id: ELITEA-0924
title: "Verify Pipeline Icon Updates Correctly After Setting a Custom Icon"
priority: medium
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418, 4686]
requirements: [EliteaAI/elitea_issues#4418, EliteaAI/elitea_issues#4686]
---
# ELITEA-0924: Verify Pipeline Icon Updates Correctly After Setting a Custom Icon

**Module:** Pipeline Creation Ux · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a custom icon is set for a pipeline, the icon in the pipeline list and header updates to reflect the custom icon correctly.

**Coverage:**
- Custom icon assignment and display in pipeline list view

## Preconditions

- Logged in
- Private project selected
- A pipeline (TC11-Icon-Pipeline from TC-11 or any existing pipeline) is available for editing
- A valid icon image is available for upload

## Test Data

- Pipeline to edit: TC11-Icon-Pipeline
- Icon image: any small PNG/JPG image (e.g., test-icon.png)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open TC11-Icon-Pipeline (or any existing pipeline) for editing | Pipeline edit form opens |
| 2 | Locate the icon/avatar area on the pipeline form | Icon or avatar placeholder is visible |
| 3 | Click on the icon area to trigger icon upload or selection | Upload dialog or icon picker opens |
| 4 | Upload or select a custom icon image (test-icon.png) | Custom icon is selected and previewed in the form |
| 5 | Click Save | Pipeline is saved with the new custom icon |
| 6 | Return to the pipelines list | Pipelines list is displayed |
| 7 | Observe the icon displayed for the edited pipeline | The pipeline displays the newly set custom icon, not the default |

## Expected Final State

The pipeline displays the newly set custom icon, not the default

## Pass/Fail Criteria

**Pass:**
- Custom icon is accepted during edit
- Pipeline list shows the custom icon after save

**Fail:**
- Custom icon is not saved or reverts to default after save
- Pipeline list still shows the default icon after custom icon was set
