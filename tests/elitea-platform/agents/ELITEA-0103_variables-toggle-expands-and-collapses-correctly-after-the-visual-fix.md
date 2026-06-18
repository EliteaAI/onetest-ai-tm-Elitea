---
id: ELITEA-0103
title: "Variables Toggle Expands and Collapses Correctly After the Visual Fix"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3833]
---
# ELITEA-0103: Variables Toggle Expands and Collapses Correctly After the Visual Fix

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the "Show variables / Hide variables" toggle on a nested agent's Tool Card remains fully functional after the CSS and height changes introduced by the fix.

**Coverage:**
- Clicking "Show variables (N)" expands the variable input fields for the nested agent
- Number of expanded input fields matches the count `N` in the toggle label
- Values entered in variable fields are retained after collapse and re-expand
- Clicking "Hide variables (N)" collapses the fields cleanly
- Variable values are preserved after saving the parent Agent and re-opening

## Preconditions

- Logged in to elitea.ai
- Private project context selected
- A **child Agent** exists with exactly **2 variables** defined in its instructions: `{{var1}}` and `{{var2}}`
- A **parent Agent** exists with that child Agent added as a nested sub-agent in TOOLKITS — the Tool Card shows "Show variables (2)"
- Browser: Chromium-based, desktop

## Test Data

| Item | Value |
|---|---|
| Parent Agent | Agent with nested child agent in TOOLKITS |
| Child Agent variables | `{{var1}}`, `{{var2}}` |
| Value for `{{var1}}` | `TestValue1` |
| Value for `{{var2}}` | `TestValue2` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the parent Agent's detail page. Open the TOOLKITS section. Locate the Tool Card for the nested child Agent showing 'Show variables (2)'. | The toggle label 'Show variables (2)' is displayed and the variable input fields are collapsed (not visible). |
| 2 | Click 'Show variables (2)'. | Exactly 2 variable input fields expand below the toggle. The toggle label changes to 'Hide variables (2)'. No layout breakage is visible. |
| 3 | Enter 'TestValue1' in the {{var1}} field and 'TestValue2' in the {{var2}} field. | Both values are accepted and displayed in their respective fields. |
| 4 | Click 'Hide variables (2)'. | The variable input area collapses cleanly. No residual DOM elements or visual artifacts remain. The toggle label returns to 'Show variables (2)'. |
| 5 | Click 'Show variables (2)' again to re-expand. | The variable fields re-expand with the previously entered values 'TestValue1' and 'TestValue2' intact. |
| 6 | Click 'Save' at the top of the parent Agent configuration page. | Agent is saved successfully. No error toast or validation message. |
| 7 | Reload the page or navigate away and return to the same parent Agent. Open TOOLKITS → expand variables. | The variable values 'TestValue1' and 'TestValue2' are persisted and displayed correctly after save and reload. |

## Expected Final State

The variable values 'TestValue1' and 'TestValue2' are persisted and displayed correctly after save and reload.

## Pass/Fail Criteria

**Pass:**
- Toggle expands exactly N variable input fields matching the count in the label
- Values entered are retained through collapse/re-expand cycles
- Variable values persist after save and page reload
- No layout breakage or visual artifacts during expand/collapse

**Fail:**
- Clicking the toggle produces no visible action
- Wrong number of variable input fields shown after expanding
- Previously entered values are lost after collapsing and re-expanding
- Variable values not persisted after save
- Layout breaks during expand/collapse
