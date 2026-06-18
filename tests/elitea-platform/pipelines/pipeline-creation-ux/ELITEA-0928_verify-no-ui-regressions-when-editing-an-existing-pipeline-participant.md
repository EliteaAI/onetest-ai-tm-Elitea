---
id: ELITEA-0928
title: "Verify No UI Regressions When Editing an Existing Pipeline Participant in Chat"
priority: high
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418]
requirements: [EliteaAI/elitea_issues#4418]
---
# ELITEA-0928: Verify No UI Regressions When Editing an Existing Pipeline Participant in Chat

**Module:** Pipeline Creation Ux · **Priority:** High · **Type:** Functional

**Objective:** Verify that editing an existing pipeline participant within a chat conversation does not produce UI regressions — all form sections load correctly and changes can be saved.

**Coverage:**
- Edit form load for existing pipeline participant in chat
- Form field availability during edit in chat context
- Save functionality for edited pipeline participant

## Preconditions

- Logged in
- Private project selected
- A chat conversation exists with at least one pipeline participant (e.g., TC16-Chat-Pipeline-Participant)

## Test Data

- Existing chat pipeline participant to edit
- Updated Welcome Message: Updated welcome message for TC17

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation that has a pipeline participant | Chat interface is displayed with the pipeline participant visible |
| 2 | Open the pipeline participant for editing | Pipeline configuration panel/canvas opens |
| 3 | Verify all configuration sections are loaded without errors: Name, Description, Tags, Welcome Message, Conversation Starters, Advanced | All sections are visible and interactive |
| 4 | Verify the scroll behavior on the configuration panel: scroll down and back up | Scrolling is smooth and reaches both top and bottom without getting stuck |
| 5 | Update the Welcome Message to 'Updated welcome message for TC17' | Field is updated |
| 6 | Click Save | Changes are saved. A success confirmation is shown |
| 7 | Re-open the pipeline participant for editing | Panel opens with the updated Welcome Message pre-populated |

## Expected Final State

Panel opens with the updated Welcome Message pre-populated

## Pass/Fail Criteria

**Pass:**
- All form sections load correctly on edit
- Scroll is fully functional in the edit panel
- Changes save successfully and are persistent

**Fail:**
- Any form section fails to load or is missing
- Scroll is broken during edit (cannot reach top or bottom)
- Changes are not persisted after save
