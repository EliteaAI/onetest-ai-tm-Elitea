---
id: ELITEA-0917
title: "Verify Editing an Existing Pipeline Has All Sections Available"
priority: critical
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418]
requirements: [EliteaAI/elitea_issues#4418]
---
# ELITEA-0917: Verify Editing an Existing Pipeline Has All Sections Available

**Module:** Pipeline Creation Ux · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that opening an already-saved pipeline for editing shows all sections (Flow, YAML, Toolkit) as immediately active without requiring another save cycle.

**Coverage:**
- Edit mode for existing pipeline
- Full section availability on open of existing pipeline

## Preconditions

- Logged in
- Private project selected
- At least one previously saved pipeline exists

## Test Data

- Use an existing saved pipeline (e.g., TC5-PostSave-Pipeline created in TC-5, or any pre-existing pipeline)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Pipelines list | List of existing pipelines is displayed |
| 2 | Open an existing pipeline for editing | Pipeline edit form opens |
| 3 | Verify the Flow editor tab/section is active and interactive | Flow editor is immediately available without requiring a save |
| 4 | Verify the YAML editor tab/section is active and interactive | YAML editor is immediately available |
| 5 | Verify the Toolkit section add buttons (+Toolkit, +MCP, +Agent, +Pipeline) are active | All add buttons are active and clickable |
| 6 | Make a minor edit (e.g., update the Description) and click Save | Save completes successfully. No sections become disabled after saving |

## Expected Final State

Save completes successfully. No sections become disabled after saving

## Pass/Fail Criteria

**Pass:**
- All sections are active when editing an existing pipeline
- Saving edits does not cause any section to become disabled

**Fail:**
- Any section is disabled when opening an existing pipeline for edit
- Saving changes causes any section to become disabled
