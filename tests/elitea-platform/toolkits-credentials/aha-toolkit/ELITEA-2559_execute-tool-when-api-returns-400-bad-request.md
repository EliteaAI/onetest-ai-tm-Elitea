---
id: ELITEA-2559
title: "Execute tool when API returns 400 Bad Request"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2559: Execute tool when API returns 400 Bad Request

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify error message clearly explains validation issue when API returns 400

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit is configured
- Tool execution will trigger 400 error (invalid parameters)

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select a tool | Tool execution fails |
| 2 | Provide invalid parameters that will cause 400 error | Error message clearly explains validation issue |
| 3 | Click RUN TOOL | 400 Bad Request error is handled gracefully |
| 4 | Observe error response | Step completes successfully |

## Expected Final State

Tool execution fails

## Pass/Fail Criteria

**Pass:**
- Tool execution fails
- Error message clearly explains validation issue
- 400 Bad Request error is handled gracefully

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
