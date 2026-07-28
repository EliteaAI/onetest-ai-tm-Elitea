---
id: ELITEA-2580
title: "Verify Form/Raw Json tabs work correctly"
priority: medium
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2580: Verify Form/Raw Json tabs work correctly

**Module:** Toolkits · **Priority:** Medium · **Type:** Functional

**Objective:** Verify Form and Raw Json tabs work correctly in toolkit configuration

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is on toolkit configuration page

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Observe default Form tab is active | Both tabs are clickable |
| 2 | Click Raw Json tab | Raw Json shows valid JSON |
| 3 | Verify JSON structure displays | Switching between tabs works smoothly |
| 4 | Click Form tab | Form view returns correctly |
| 5 | Verify form view returns | Tab switching is seamless |

## Expected Final State

Both tabs are clickable, Raw Json shows valid JSON, and switching between tabs works smoothly.

## Pass/Fail Criteria

**Pass:**
- Both tabs are clickable
- Raw Json shows valid JSON
- Switching between tabs works smoothly

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
