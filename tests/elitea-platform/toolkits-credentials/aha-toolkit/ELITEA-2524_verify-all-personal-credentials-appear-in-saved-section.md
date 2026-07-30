---
id: ELITEA-2524
title: "Verify all personal credentials appear in SAVED section"
priority: high
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2524: Verify all personal credentials appear in SAVED section

**Module:** Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify all personal credentials appear in SAVED AHA CREDENTIALS section

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User has created multiple personal Aha! credentials

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to toolkit configuration page | All personal credentials are visible in dropdown |
| 2 | Open Aha Configuration dropdown | Credentials are distinguishable by Display Name |
| 3 | Scroll through SAVED AHA CREDENTIALS section | Step completes successfully |
| 4 | Verify all personal credentials are listed | Step completes successfully |

## Expected Final State

All personal credentials are visible in dropdown

## Pass/Fail Criteria

**Pass:**
- All personal credentials are visible in dropdown
- Credentials are distinguishable by Display Name

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
