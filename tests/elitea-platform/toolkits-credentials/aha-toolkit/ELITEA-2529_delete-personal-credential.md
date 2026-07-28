---
id: ELITEA-2529
title: "Delete personal credential"
priority: high
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2529: Delete personal credential

**Module:** Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify user can delete personal credential

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User has at least one personal credential that is not in use

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials page | Delete confirmation dialog appears |
| 2 | Locate personal credential to delete | Credential is deleted after confirmation |
| 3 | Click delete/remove option | Success message displays |
| 4 | Confirm deletion if prompted | Step completes successfully |
| 5 | Observe result | Step completes successfully |

## Expected Final State

Delete confirmation dialog appears

## Pass/Fail Criteria

**Pass:**
- Delete confirmation dialog appears
- Credential is deleted after confirmation
- Success message displays

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
