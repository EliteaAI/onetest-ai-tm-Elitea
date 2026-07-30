---
id: ELITEA-2522
title: "Verify JSON response format is correct"
priority: critical
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2522: Verify JSON response format is correct

**Module:** Toolkits · **Priority:** Critical · **Type:** Functional

**Objective:** Verify tool execution returns correct and parseable JSON response format

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Aha! toolkit is configured and saved
- Any tool is enabled

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open saved Aha! toolkit TEST SETTINGS | Response is valid JSON format |
| 2 | Select any tool from dropdown | JSON can be parsed without errors |
| 3 | Click RUN TOOL | Response structure matches expected format |
| 4 | Observe response format | Step completes successfully |
| 5 | Verify JSON structure is valid | Step completes successfully |

## Expected Final State

Response is valid JSON format

## Pass/Fail Criteria

**Pass:**
- Response is valid JSON format
- JSON can be parsed without errors
- Response structure matches expected format

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
