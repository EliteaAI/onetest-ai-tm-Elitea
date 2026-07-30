---
id: ELITEA-2562
title: "Execute tool when API returns 500 Internal Server Error"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2562: Execute tool when API returns 500 Internal Server Error

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify error message indicates server-side issue for 500 errors

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit is configured

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Execute tool when Aha! API is experiencing issues (if possible to simulate) | Tool execution fails |
| 2 | Observe error response | Error message indicates server-side issue |

## Expected Final State

Tool execution fails

## Pass/Fail Criteria

**Pass:**
- Tool execution fails
- Error message indicates server-side issue
- 500 error is handled appropriately
- User is not shown raw error details

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
