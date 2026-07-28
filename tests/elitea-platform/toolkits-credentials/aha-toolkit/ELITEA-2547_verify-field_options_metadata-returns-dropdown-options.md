---
id: ELITEA-2547
title: "Verify field_options_metadata returns dropdown options"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2547: Verify field_options_metadata returns dropdown options

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify field_options_metadata tool returns dropdown options for fields

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit is configured with field_options_metadata tool

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select field_options_metadata tool | Tool executes successfully |
| 2 | Provide field identifier | Field options/dropdown values are returned |
| 3 | Click RUN TOOL | Response format is correct |
| 4 | Observe response | Step completes successfully |
| 5 | Verify options are returned | Step completes successfully |

## Expected Final State

Tool executes successfully

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- Field options/dropdown values are returned
- Response format is correct

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
