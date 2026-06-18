---
id: ELITEA-0929
title: "Verify New Pipeline Creation Form Displays Only Basic Configuration Fields"
priority: critical
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418]
requirements: [EliteaAI/elitea_issues#4418]
---
# ELITEA-0929: Verify New Pipeline Creation Form Displays Only Basic Configuration Fields

**Module:** Pipeline Creation Ux · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that opening the Create New Pipeline form presents only the basic metadata fields and that no advanced editing sections are shown.

**Coverage:**
- Form field visibility on initial creation state
- Absence of Flow editor, YAML editor, and Toolkit section on first open

## Preconditions

- Logged in
- Private project selected
- At least one existing pipeline present in the project (for comparison)

## Test Data

- Pipeline Name: TC1-Pipeline-Test
- Description: Test description for TC1

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Pipelines section from the sidebar | Pipelines list page is displayed |
| 2 | Click 'Create New Pipeline' (or equivalent '+' button) | New pipeline creation form opens |
| 3 | Observe all visible fields and sections on the form | The following fields are visible: Name, Description, Tags, Welcome Message, Conversation Starters, Advanced (Step limit) |
| 4 | Check whether the Flow editor tab/section is visible and interactive | Flow editor is not visible or is clearly disabled/grayed out |
| 5 | Check whether the YAML editor tab/section is visible and interactive | YAML editor is not visible or is clearly disabled/grayed out |
| 6 | Check whether the Toolkits section (with +Toolkit, +MCP, +Agent, +Pipeline buttons) is present and interactive | Toolkit section add buttons are not visible or are clearly disabled/grayed out |

## Expected Final State

Toolkit section add buttons are not visible or are clearly disabled/grayed out

## Pass/Fail Criteria

**Pass:**
- Only Name, Description, Tags, Welcome Message, Conversation Starters, and Advanced (Step limit) fields are visible and active
- Flow editor, YAML editor, and Toolkit add buttons are disabled or absent

**Fail:**
- Flow editor, YAML editor, or Toolkit add buttons are active and clickable before first save
- Any additional unexpected section is visible
