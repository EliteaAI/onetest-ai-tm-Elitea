---
id: ELITEA-2520
title: "Verify read_records tool executes successfully"
priority: critical
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2520: Verify read_records tool executes successfully

**Module:** Toolkits · **Priority:** Critical · **Type:** Functional

**Objective:** Verify read_records tool executes successfully and returns record details

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Aha! toolkit is configured with valid credentials
- read_records tool is enabled
- Valid record ID is available

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open saved Aha! toolkit TEST SETTINGS | Tool executes successfully |
| 2 | Select read_records from tool dropdown | JSON response with record details is returned |
| 3 | Provide record ID parameter | Step completes successfully |
| 4 | Click RUN TOOL | Step completes successfully |
| 5 | Wait for execution | Step completes successfully |
| 6 | Observe response | Step completes successfully |

## Expected Final State

Tool executes successfully

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- JSON response with record details is returned

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
