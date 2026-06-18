---
id: ELITEA-0913
title: "Verify Flow and YAML Editors Are Disabled/Hidden Before First Save"
priority: critical
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418]
requirements: [EliteaAI/elitea_issues#4418]
---
# ELITEA-0913: Verify Flow and YAML Editors Are Disabled/Hidden Before First Save

**Module:** Pipeline Creation Ux · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that both the Flow editor and YAML editor are non-interactive until the pipeline is saved for the first time.

**Coverage:**
- Flow editor disabled/hidden state before save
- YAML editor disabled/hidden state before save
- Attempted interaction with disabled editors

## Preconditions

- Logged in
- Private project selected
- New pipeline creation form opened (not yet saved)

## Test Data

- Pipeline Name: TC2-Pipeline-FlowYAML
- Description: Test description TC2

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Create New Pipeline form | Form is displayed with basic fields |
| 2 | Locate the Flow editor tab or section | Flow editor tab/section is either hidden or visually disabled (grayed out, not clickable) |
| 3 | Attempt to click on the Flow editor tab/section | Either nothing happens, a tooltip explains it will be available after save, or the tab is not clickable |
| 4 | Locate the YAML editor tab or section | YAML editor tab/section is either hidden or visually disabled |
| 5 | Attempt to click on the YAML editor tab/section | Either nothing happens, a tooltip explains it will be available after save, or the tab is not clickable |
| 6 | Enter Name (TC2-Pipeline-FlowYAML) and Description, then click Save | Pipeline is saved successfully. A success confirmation is shown |
| 7 | After successful save, check the Flow editor tab/section | Flow editor is now active and interactive |
| 8 | After successful save, check the YAML editor tab/section | YAML editor is now active and interactive |

## Expected Final State

YAML editor is now active and interactive

## Pass/Fail Criteria

**Pass:**
- Flow and YAML editors are non-interactive before save
- Both editors become active immediately after first successful save

**Fail:**
- Either editor is interactive before the pipeline is saved
- Either editor remains disabled after a successful save
