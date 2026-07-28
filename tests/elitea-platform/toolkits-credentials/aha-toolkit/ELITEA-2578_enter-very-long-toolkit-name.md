---
id: ELITEA-2578
title: "Enter very long Toolkit Name"
priority: medium
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2578: Enter very long Toolkit Name

**Module:** Toolkits · **Priority:** Medium · **Type:** Functional

**Objective:** Verify field handles long Toolkit Name appropriately

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is creating toolkit

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/
- Very long name: 200+ characters

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enter Toolkit Name with 200+ characters | Field accepts long input OR enforces character limit |
| 2 | Observe field behavior | If saved, name displays with truncation in lists |
| 3 | Attempt to save | Save completes or validation occurs |
| 4 | Verify toolkit saves or validation occurs | Appropriate handling of long input |

## Expected Final State

Field accepts long input OR enforces character limit, and if saved, name displays with truncation in lists.

## Pass/Fail Criteria

**Pass:**
- Field accepts long input OR enforces character limit
- If saved, name displays with truncation in lists

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
