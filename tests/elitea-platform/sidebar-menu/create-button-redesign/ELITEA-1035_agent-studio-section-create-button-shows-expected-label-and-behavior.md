---
id: ELITEA-1035
title: "Agent Studio Section: Create Button Shows Expected Label and Behavior"
priority: high
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1035: Agent Studio Section: Create Button Shows Expected Label and Behavior

**Module:** Create Button Redesign · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Create button in the Agent Studio section displays the expected label and behavior per Figma design.

**Coverage:**
- Create button label on Agent Studio
- Button click and dropdown action

## Preconditions

- Logged in to ELITEA
- Sidebar in expanded state

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agent Studio from the sidebar | Agent Studio page loads |
| 2 | Inspect the Create button label in the sidebar | Button shows the expected label per Figma design (dropdown-list style, no entity label) |
| 3 | Click the Create button or its dropdown arrow | Dropdown opens with all available entity types |
| 4 | Select any entity from the dropdown | Navigation proceeds to the correct creation form |

## Expected Final State

Navigation proceeds to the correct creation form

## Pass/Fail Criteria

**Pass:**
- Agent Studio Create button matches Figma-specified label and behavior

**Fail:**
- Button shows wrong label
- Button is missing or non-functional on Agent Studio page
