---
id: ELITEA-2574
title: "Execute tool that returns large JSON response"
priority: medium
type: performance
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2574: Execute tool that returns large JSON response

**Module:** Toolkits · **Priority:** Medium · **Type:** Performance

**Objective:** Verify response displays without performance degradation for large datasets

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit is configured
- Tool will return 500+ records

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select list tool likely to return many records | Large JSON response is returned |
| 2 | Click RUN TOOL | UI remains responsive |
| 3 | Wait for response | No browser freezing or crashes |
| 4 | Observe UI performance | Response displays successfully |

## Expected Final State

Large JSON response is returned and UI remains responsive with no browser freezing or crashes.

## Pass/Fail Criteria

**Pass:**
- Large JSON response is returned
- UI remains responsive
- No browser freezing or crashes

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
