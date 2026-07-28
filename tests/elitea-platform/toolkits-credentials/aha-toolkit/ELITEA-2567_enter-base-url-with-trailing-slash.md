---
id: ELITEA-2567
title: "Enter Base URL with trailing slash"
priority: medium
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2567: Enter Base URL with trailing slash

**Module:** Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify system handles URL normalization correctly

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is creating Aha! credential

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open credential form | System accepts URL with trailing slash |
| 2 | Enter Base URL with trailing slash: https://subdomain.aha.io/ | URL is normalized (trailing slash removed) |
| 3 | Save credential | Credential saves successfully |
| 4 | Verify URL is normalized | Step completes successfully |

## Expected Final State

System accepts URL with trailing slash

## Pass/Fail Criteria

**Pass:**
- System accepts URL with trailing slash
- URL is normalized (trailing slash removed)
- Credential saves successfully

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
