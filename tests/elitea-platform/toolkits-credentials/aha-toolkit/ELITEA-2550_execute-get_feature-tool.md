---
id: ELITEA-2550
title: "Execute get_feature tool"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2550: Execute get_feature tool

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify get_feature tool retrieves feature data

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit configured with get_feature tool
- Valid feature ID available

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select get_feature tool | Tool executes successfully |
| 2 | Provide feature ID | Feature data is returned |
| 3 | Click RUN TOOL | Response includes feature details |
| 4 | Observe response | Step completes successfully |

## Expected Final State

Tool executes successfully

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- Feature data is returned
- Response includes feature details

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
