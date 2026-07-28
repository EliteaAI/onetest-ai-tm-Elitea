---
id: ELITEA-2570
title: "View project credential from different user account"
priority: medium
type: security
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2570: View project credential from different user account

**Module:** Credentials · **Priority:** Medium · **Type:** Security

**Objective:** Verify API Key remains masked when viewed by other users

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Project credential exists
- User B is viewing User A's project credential

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As User A, create project credential | API Key is masked for User B |
| 2 | Log in as User B | API Key value is not exposed |
| 3 | View project credential in dropdown or credentials page | Step completes successfully |
| 4 | Observe API Key field | Step completes successfully |

## Expected Final State

API Key is masked for User B

## Pass/Fail Criteria

**Pass:**
- API Key is masked for User B
- API Key value is not exposed

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
