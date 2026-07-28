---
id: ELITEA-2555
title: "Execute get_epic tool"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2555: Execute get_epic tool

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify get_epic tool retrieves epic data

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit configured with get_epic tool
- Valid epic ID available

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select get_epic tool | Tool executes successfully |
| 2 | Provide epic ID | Epic data is returned |
| 3 | Click RUN TOOL | Step completes successfully |
| 4 | Observe response | Step completes successfully |

## Expected Final State

Tool executes successfully

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- Epic data is returned

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
