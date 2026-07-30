---
id: ELITEA-2538
title: "Select individual tools"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2538: Select individual tools

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify user can select individual tools (Add comment, Attach file, Copy record, etc.)

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is on toolkit configuration page

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to TOOLS section | Selected tools show checked state |
| 2 | Check "Add comment" checkbox | Unselected tools remain unchecked |
| 3 | Check "Attach file" checkbox | Selection is responsive |
| 4 | Check "Copy record" checkbox | Step completes successfully |
| 5 | Leave other tools unchecked | Step completes successfully |

## Expected Final State

Selected tools show checked state

## Pass/Fail Criteria

**Pass:**
- Selected tools show checked state
- Unselected tools remain unchecked
- Selection is responsive

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
