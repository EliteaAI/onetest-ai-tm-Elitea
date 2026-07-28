---
id: ELITEA-2506
title: "Verify New project aha credentials option in dropdown"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2506: Verify New project aha credentials option in dropdown

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify "New project aha credentials" option is available in dropdown

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User logged in to Elitea application
- User is on New Aha! Toolkit configuration page

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to New Aha! Toolkit configuration page | CREATE section is visible |
| 2 | Click on "Aha Configuration" dropdown field | Both "New private aha credentials" and "New project aha credentials" options are present |
| 3 | Observe the dropdown options | Step completes successfully |
| 4 | Verify CREATE section exists | Step completes successfully |
| 5 | Verify both private and project credential options exist | Step completes successfully |

## Expected Final State

CREATE section is visible

## Pass/Fail Criteria

**Pass:**
- CREATE section is visible
- Both "New private aha credentials" and "New project aha credentials" options are present

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
