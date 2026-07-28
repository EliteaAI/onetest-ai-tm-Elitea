---
id: ELITEA-2545
title: "Verify copy_record tool copies record between projects"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2545: Verify copy_record tool copies record between projects

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify copy_record tool successfully copies record between projects

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit is configured with copy_record tool
- Source and destination projects exist

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select copy_record tool | Tool executes successfully |
| 2 | Provide source record ID and destination project | Record is copied to destination project |
| 3 | Click RUN TOOL | Response confirms successful copy |
| 4 | Verify success response | Step completes successfully |
| 5 | Check destination project in Aha! | Step completes successfully |

## Expected Final State

Tool executes successfully

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- Record is copied to destination project
- Response confirms successful copy

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
