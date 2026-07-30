---
id: ELITEA-2508
title: "Verify project credential appears in shared list"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2508: Verify project credential appears in shared list

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify project-level credential appears in shared credential list

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User A created a project-level Aha! credential
- User B is a member of the same project

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As User A, create project credential "Shared Project Credential" | Credential is visible to User A |
| 2 | Navigate to Aha Configuration dropdown as User A | Credential IS visible to User B |
| 3 | Verify credential appears in SAVED AHA CREDENTIALS | Step completes successfully |
| 4 | Log out from User A | Step completes successfully |
| 5 | Log in as User B | Step completes successfully |
| 6 | Navigate to Aha Configuration dropdown as User B | Step completes successfully |
| 7 | Look for "Shared Project Credential" | Step completes successfully |

## Expected Final State

Credential is visible to User A

## Pass/Fail Criteria

**Pass:**
- Credential is visible to User A
- Credential IS visible to User B

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
