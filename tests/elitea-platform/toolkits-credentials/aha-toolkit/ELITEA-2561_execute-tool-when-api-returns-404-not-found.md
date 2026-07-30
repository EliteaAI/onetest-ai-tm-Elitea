---
id: ELITEA-2561
title: "Execute tool when API returns 404 Not Found"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2561: Execute tool when API returns 404 Not Found

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify error message indicates resource not found for 404 errors

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit is configured

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select a tool | Tool execution fails |
| 2 | Provide record ID that doesn't exist | Error message indicates resource not found |
| 3 | Click RUN TOOL | 404 error is handled gracefully |
| 4 | Observe error response | Step completes successfully |

## Expected Final State

Tool execution fails

## Pass/Fail Criteria

**Pass:**
- Tool execution fails
- Error message indicates resource not found
- 404 error is handled gracefully

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
