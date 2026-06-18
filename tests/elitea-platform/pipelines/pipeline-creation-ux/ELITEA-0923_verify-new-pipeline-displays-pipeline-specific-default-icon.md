---
id: ELITEA-0923
title: "Verify New Pipeline Displays Pipeline-Specific Default Icon"
priority: medium
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418, 4686]
requirements: [EliteaAI/elitea_issues#4418, EliteaAI/elitea_issues#4686]
---
# ELITEA-0923: Verify New Pipeline Displays Pipeline-Specific Default Icon

**Module:** Pipeline Creation Ux · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a newly created pipeline displays the pipeline-specific default icon (a rounded square icon with a node/network graph symbol, as defined for pipelines) and not the agent default icon.

**Coverage:**
- Default icon assignment on pipeline creation
- Visual distinction between pipeline-specific and agent default icons

## Preconditions

- Logged in
- Private project selected
- At least one agent exists (to compare default icon appearance)

## Test Data

- New pipeline: Name TC11-Icon-Pipeline, Description TC11 icon test

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents list and observe the default icon for any agent with no custom icon set | Agent default icon is noted (for comparison) |
| 2 | Navigate to the Pipelines section | Pipelines list is displayed |
| 3 | Create a new pipeline: Name TC11-Icon-Pipeline, Description TC11 icon test. Click Save | Pipeline is created successfully |
| 4 | Observe the icon displayed for TC11-Icon-Pipeline in the pipelines list | The pipeline displays the pipeline-specific default icon: a rounded square icon featuring a node/network graph symbol |
| 5 | Compare the pipeline icon with the agent default icon noted in step 1 | Icons are visually distinct — pipeline icon shows a node/network graph symbol; agent icon shows a different symbol |
| 6 | Open the pipeline in edit mode and observe the icon in the form header | The same pipeline-specific node/network graph icon is shown in the form header |

## Expected Final State

The same pipeline-specific node/network graph icon is shown in the form header

## Pass/Fail Criteria

**Pass:**
- New pipeline displays the pipeline-specific default icon (rounded square with node/network graph symbol)
- Pipeline icon is visually distinct from the agent default icon

**Fail:**
- New pipeline displays the agent default icon instead of the pipeline-specific icon
- Pipeline icon is identical in appearance to the agent default icon
