---
id: ELITEA-2554
title: "Execute get_initiative tool"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2554: Execute get_initiative tool

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify get_initiative tool retrieves initiative data

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit configured with get_initiative tool
- Valid initiative ID available

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select get_initiative tool | Tool executes successfully |
| 2 | Provide initiative ID | Initiative data is returned |
| 3 | Click RUN TOOL | Step completes successfully |
| 4 | Observe response | Step completes successfully |

## Expected Final State

Tool executes successfully

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- Initiative data is returned

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
