---
id: ELITEA-2519
title: "Verify search_records tool executes successfully"
priority: critical
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2519: Verify search_records tool executes successfully

**Module:** Toolkits · **Priority:** Critical · **Type:** Functional

**Objective:** Verify search_records tool executes successfully with valid search parameters

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Aha! toolkit is configured and saved
- search_records tool is enabled

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open saved Aha! toolkit TEST SETTINGS | Tool executes successfully |
| 2 | Select search_records from tool dropdown | JSON response with search results is returned |
| 3 | Provide search parameters if required | No errors occur |
| 4 | Click RUN TOOL button | Step completes successfully |
| 5 | Wait for tool execution | Step completes successfully |
| 6 | Observe response | Step completes successfully |

## Expected Final State

Tool executes successfully

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- JSON response with search results is returned
- No errors occur

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
