---
id: ELITEA-2523
title: "Create multiple personal credentials"
priority: high
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2523: Create multiple personal credentials

**Module:** Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify user can create multiple personal credentials with different Display Names

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User logged in to Elitea application

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create first personal credential "Personal Cred 1" | All three credentials are created successfully |
| 2 | Save successfully | All credentials appear in credential list |
| 3 | Create second personal credential "Personal Cred 2" | Each has unique Display Name and ID |
| 4 | Save successfully | Step completes successfully |
| 5 | Create third personal credential "Personal Cred 3" | Step completes successfully |
| 6 | Save successfully | Step completes successfully |
| 7 | Navigate to Credentials page | Step completes successfully |

## Expected Final State

All three credentials are created successfully

## Pass/Fail Criteria

**Pass:**
- All three credentials are created successfully
- All credentials appear in credential list
- Each has unique Display Name and ID

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
