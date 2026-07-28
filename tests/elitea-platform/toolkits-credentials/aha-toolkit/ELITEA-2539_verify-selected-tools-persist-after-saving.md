---
id: ELITEA-2539
title: "Verify selected tools persist after saving"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2539: Verify selected tools persist after saving

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify selected tools persist after saving toolkit

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User has selected specific tools

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select tools: Add comment, Search, Read records | Toolkit saves successfully |
| 2 | Enter Toolkit Name | Previously selected tools remain checked |
| 3 | Select credential | Unselected tools remain unchecked |
| 4 | Click Save | Step completes successfully |
| 5 | Re-open saved toolkit | Step completes successfully |
| 6 | Verify tool selections | Step completes successfully |

## Expected Final State

Toolkit saves successfully

## Pass/Fail Criteria

**Pass:**
- Toolkit saves successfully
- Previously selected tools remain checked
- Unselected tools remain unchecked

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
