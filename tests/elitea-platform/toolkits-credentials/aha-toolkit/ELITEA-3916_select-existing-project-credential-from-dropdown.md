---
id: ELITEA-3916
title: "Select existing project credential from dropdown"
priority: critical
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-3916: Select existing project credential from dropdown

**Module:** Toolkits · **Priority:** Critical · **Type:** Functional

**Objective:** Verify user can select existing project credential from dropdown

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- At least one project-level credential exists
- User is on New Aha! Toolkit configuration page

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to New Aha! Toolkit configuration page | Project credentials are visible in dropdown |
| 2 | Click Aha Configuration dropdown | Project credential is selectable |
| 3 | Verify project credentials appear in SAVED AHA CREDENTIALS | Selected credential shows in field |
| 4 | Select project credential from list | Step completes successfully |
| 5 | Verify credential is selected | Step completes successfully |

## Expected Final State

Project credentials are visible in dropdown

## Pass/Fail Criteria

**Pass:**
- Project credentials are visible in dropdown
- Project credential is selectable
- Selected credential shows in field

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
