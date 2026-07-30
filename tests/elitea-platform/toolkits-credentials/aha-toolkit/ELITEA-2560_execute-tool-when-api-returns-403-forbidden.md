---
id: ELITEA-2560
title: "Execute tool when API returns 403 Forbidden"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2560: Execute tool when API returns 403 Forbidden

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify error message indicates permission/access issue for 403 errors

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit is configured
- Credentials lack necessary permissions

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select a tool requiring specific permissions | Tool execution fails |
| 2 | Click RUN TOOL | Error message indicates permission/access issue |
| 3 | Observe error response | 403 Forbidden error is handled appropriately |

## Expected Final State

Tool execution fails

## Pass/Fail Criteria

**Pass:**
- Tool execution fails
- Error message indicates permission/access issue
- 403 Forbidden error is handled appropriately

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
