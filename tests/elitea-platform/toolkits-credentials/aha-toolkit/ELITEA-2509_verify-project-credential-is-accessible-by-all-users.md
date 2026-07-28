---
id: ELITEA-2509
title: "Verify project credential is accessible by all users"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2509: Verify project credential is accessible by all users

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify project-level credential can be used by all users within the project

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User A created project credential "Project Credential 1"
- User B is a member of same project

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As User B, navigate to New Aha! Toolkit configuration page | User B can see and select User A's project credential |
| 2 | Open Aha Configuration dropdown | Toolkit saves successfully using project credential |
| 3 | Verify "Project Credential 1" appears | Step completes successfully |
| 4 | Select "Project Credential 1" | Step completes successfully |
| 5 | Enter Toolkit Name: "User B Test Toolkit" | Step completes successfully |
| 6 | Select desired tools | Step completes successfully |
| 7 | Click Save button | Step completes successfully |

## Expected Final State

User B can see and select User A's project credential

## Pass/Fail Criteria

**Pass:**
- User B can see and select User A's project credential
- Toolkit saves successfully using project credential

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
