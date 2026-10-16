---
id: ELITEA-3911
title: "Verify personal credential appears in user's list only"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-3911: Verify personal credential appears in user's list only

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify personal credential appears only in the creating user's credential list

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User A created a personal Aha! credential
- Access to User B account (different user in same project)

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As User A, create personal Aha! credential "User A Personal" | "User A Personal" credential is visible in User A's list |
| 2 | Navigate to Credentials page as User A | "User A Personal" credential does NOT appear in User B's list |
| 3 | Verify "User A Personal" credential appears in list | Step completes successfully |
| 4 | Log out from User A | Step completes successfully |
| 5 | Log in as User B | Step completes successfully |
| 6 | Navigate to Credentials page as User B | Step completes successfully |
| 7 | Search for "User A Personal" credential in list | Step completes successfully |

## Expected Final State

"User A Personal" credential is visible in User A's list

## Pass/Fail Criteria

**Pass:**
- "User A Personal" credential is visible in User A's list
- "User A Personal" credential does NOT appear in User B's list

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
