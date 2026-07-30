---
id: ELITEA-2553
title: "Execute get_release tool"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2553: Execute get_release tool

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify get_release tool retrieves release data

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit configured with get_release tool
- Valid release ID available

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select get_release tool | Tool executes successfully |
| 2 | Provide release ID | Release data is returned |
| 3 | Click RUN TOOL | Step completes successfully |
| 4 | Observe response | Step completes successfully |

## Expected Final State

Tool executes successfully

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- Release data is returned

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
