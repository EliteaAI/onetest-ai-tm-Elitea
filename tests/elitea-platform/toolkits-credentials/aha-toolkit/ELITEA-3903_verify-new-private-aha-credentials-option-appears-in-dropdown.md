---
id: ELITEA-3903
title: "Verify New private aha credentials option appears in dropdown"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-3903: Verify New private aha credentials option appears in dropdown

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify "New private aha credentials" option is available in Aha Configuration dropdown

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
| 1 | Navigate to New Aha! Toolkit configuration page | Dropdown opens and displays options |
| 2 | Click on "Aha Configuration" dropdown field | CREATE section is visible at the top of dropdown |
| 3 | Observe the dropdown options | "New private aha credentials" option is present with appropriate icon |
| 4 | Verify CREATE section exists at top of dropdown | Step completes successfully |
| 5 | Verify "New private aha credentials" option exists | Step completes successfully |

## Expected Final State

Dropdown opens and displays options

## Pass/Fail Criteria

**Pass:**
- Dropdown opens and displays options
- CREATE section is visible at the top of dropdown
- "New private aha credentials" option is present with appropriate icon

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
