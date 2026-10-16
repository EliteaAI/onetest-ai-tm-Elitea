---
id: ELITEA-3915
title: "Select existing personal credential from dropdown"
priority: critical
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-3915: Select existing personal credential from dropdown

**Module:** Toolkits · **Priority:** Critical · **Type:** Functional

**Objective:** Verify user can select existing personal credential from Aha Configuration dropdown

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User has at least one saved personal Aha! credential
- User is on New Aha! Toolkit configuration page

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to New Aha! Toolkit configuration page | Dropdown displays saved credentials |
| 2 | Click Aha Configuration dropdown | Personal credential is selectable |
| 3 | Verify SAVED AHA CREDENTIALS section shows existing credentials | Selected credential shows in field |
| 4 | Select personal credential from list | Step completes successfully |
| 5 | Verify credential is selected | Step completes successfully |

## Expected Final State

Dropdown displays saved credentials

## Pass/Fail Criteria

**Pass:**
- Dropdown displays saved credentials
- Personal credential is selectable
- Selected credential shows in field

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
