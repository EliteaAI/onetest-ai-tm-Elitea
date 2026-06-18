---
id: ELITEA-0914
title: "Verify Toolkit Section Add Buttons Are Hidden Before First Save and Visible After"
priority: critical
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418]
requirements: [EliteaAI/elitea_issues#4418]
---
# ELITEA-0914: Verify Toolkit Section Add Buttons Are Hidden Before First Save and Visible After

**Module:** Pipeline Creation Ux · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Toolkit section add buttons (+Toolkit, +MCP, +Agent, +Pipeline) are completely hidden (not rendered) before the new pipeline is saved for the first time, and become visible only after a successful save.

**Coverage:**
- Toolkit section completely hidden before first save
- Toolkit section becomes visible and functional after first save

## Preconditions

- Logged in
- Private project selected
- New pipeline creation form is open (not yet saved)

## Test Data

- Pipeline Name: TC3-Pipeline-Toolkits
- Description: Test description TC3

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Create New Pipeline form | Form is displayed with basic metadata fields |
| 2 | Scroll through the entire form from top to bottom | Only the following sections/fields are visible: Name, Description, Tags, Welcome Message, Conversation Starters, Advanced (Step limit) |
| 3 | Verify the Toolkit section is not present anywhere on the form | The Toolkit section (including +Toolkit, +MCP, +Agent, +Pipeline buttons) is completely absent — not rendered in the DOM or visible in the UI |
| 4 | Enter Name (TC3-Pipeline-Toolkits) and Description (Test description TC3). Click Save | Pipeline is saved successfully. Success confirmation is displayed |
| 5 | After save, scroll through the pipeline edit form | The Toolkit section is now visible in the UI |
| 6 | Verify the +Toolkit, +MCP, +Agent, +Pipeline buttons are visible and clickable | All four add buttons are displayed and interactive |
| 7 | Click one of the add buttons (e.g., +Toolkit) | A toolkit selection dialog or picker opens without error |

## Expected Final State

A toolkit selection dialog or picker opens without error

## Pass/Fail Criteria

**Pass:**
- The entire Toolkit section is not displayed at any point before the first save
- Toolkit section with all add buttons appears immediately after the first successful save
- All add buttons are functional post-save

**Fail:**
- The Toolkit section or any of its add buttons are visible before the pipeline is saved (even if disabled/grayed out)
- Toolkit section does not appear after a successful save
- Any add button does not function after save
