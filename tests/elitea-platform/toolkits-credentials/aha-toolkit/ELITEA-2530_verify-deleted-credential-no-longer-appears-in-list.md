---
id: ELITEA-2530
title: "Verify deleted credential no longer appears in list"
priority: high
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2530: Verify deleted credential no longer appears in list

**Module:** Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify deleted credential no longer appears in credential list

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User has deleted a credential

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Delete a credential | Deleted credential does not appear in Credentials page |
| 2 | Navigate to Credentials page | Deleted credential does not appear in dropdown lists |
| 3 | Search for deleted credential | Step completes successfully |
| 4 | Open Aha Configuration dropdown | Step completes successfully |
| 5 | Verify credential is not in SAVED section | Step completes successfully |

## Expected Final State

Deleted credential does not appear in Credentials page

## Pass/Fail Criteria

**Pass:**
- Deleted credential does not appear in Credentials page
- Deleted credential does not appear in dropdown lists

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
