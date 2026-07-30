---
id: ELITEA-2526
title: "Verify all project credentials appear in SAVED section"
priority: high
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2526: Verify all project credentials appear in SAVED section

**Module:** Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify all project credentials appear in SAVED AHA CREDENTIALS section

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Multiple project-level credentials exist

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to toolkit configuration page | All project credentials are visible |
| 2 | Open Aha Configuration dropdown | Credentials are clearly labeled |
| 3 | Look through SAVED AHA CREDENTIALS section | Step completes successfully |
| 4 | Verify all project credentials are listed | Step completes successfully |

## Expected Final State

All project credentials are visible

## Pass/Fail Criteria

**Pass:**
- All project credentials are visible
- Credentials are clearly labeled

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
