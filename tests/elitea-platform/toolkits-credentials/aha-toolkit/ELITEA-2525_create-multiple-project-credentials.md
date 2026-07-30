---
id: ELITEA-2525
title: "Create multiple project credentials"
priority: high
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2525: Create multiple project credentials

**Module:** Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify user can create multiple project credentials with different Display Names

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User logged in to Elitea application
- User is working within project context

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create first project credential "Project Cred 1" | Both credentials are created successfully |
| 2 | Save successfully | Both credentials appear in shared credential list |
| 3 | Create second project credential "Project Cred 2" | Step completes successfully |
| 4 | Save successfully | Step completes successfully |
| 5 | Navigate to Credentials page | Step completes successfully |

## Expected Final State

Both credentials are created successfully

## Pass/Fail Criteria

**Pass:**
- Both credentials are created successfully
- Both credentials appear in shared credential list

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
