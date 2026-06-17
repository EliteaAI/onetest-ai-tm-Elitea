---
id: ELITEA-0925
title: "Verify Agent Creation and Editing Workflow — Regression After Pipeline UX Refactor"
priority: critical
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418]
requirements: [EliteaAI/elitea_issues#4418]
---
# ELITEA-0925: Verify Agent Creation and Editing Workflow — Regression After Pipeline UX Refactor

**Module:** Pipeline Creation Ux · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that creating and editing an Agent is not negatively impacted by the Pipeline UX refactor — form, save, flow editor, and toolkit sections all work as expected.

**Coverage:**
- Agent creation form and save
- Flow editor access in Agent
- Toolkit section access in Agent
- Full agent creation workflow regression

## Preconditions

- Logged in
- Private project selected

## Test Data

- Agent Name: TC14-Regression-Agent
- Description: Regression test for TC14

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents section from the sidebar | Agents list is displayed |
| 2 | Click 'Create New Agent' | Agent creation form opens with all standard fields |
| 3 | Enter Name (TC14-Regression-Agent) and Description (Regression test for TC14) | Fields are populated |
| 4 | Verify the Instructions/Prompt field is visible and editable | Instructions field is accessible |
| 5 | Click Save | Agent is saved successfully. No errors |
| 6 | After save, verify Toolkit section buttons are active | Toolkit add buttons are present and clickable |
| 7 | Open an existing agent for editing | Agent edit form opens with all sections active |
| 8 | Make a minor edit (e.g., update description) and save | Edit saves without error. All sections remain active |

## Expected Final State

Edit saves without error. All sections remain active

## Pass/Fail Criteria

**Pass:**
- New agent can be created and saved without error
- Toolkit section is active after save
- Existing agent can be edited and saved normally

**Fail:**
- Agent creation fails after the pipeline UX refactor
- Any section of the agent form is unexpectedly disabled
- Editing an existing agent produces errors
