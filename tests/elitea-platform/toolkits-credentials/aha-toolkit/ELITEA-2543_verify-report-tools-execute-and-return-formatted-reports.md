---
id: ELITEA-2543
title: "Verify report tools execute and return formatted reports"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2543: Verify report tools execute and return formatted reports

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify report tools execute successfully and return formatted reports

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit is configured with report tools enabled

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select a report tool from TEST SETTINGS | Report tool executes successfully |
| 2 | Provide required parameters | Formatted report data is returned |
| 3 | Click RUN TOOL | Report structure is valid |
| 4 | Wait for report generation | Step completes successfully |
| 5 | Observe response format | Step completes successfully |

## Expected Final State

Report tool executes successfully

## Pass/Fail Criteria

**Pass:**
- Report tool executes successfully
- Formatted report data is returned
- Report structure is valid

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
