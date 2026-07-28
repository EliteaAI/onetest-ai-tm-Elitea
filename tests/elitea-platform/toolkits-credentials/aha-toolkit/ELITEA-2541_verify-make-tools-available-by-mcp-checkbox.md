---
id: ELITEA-2541
title: "Verify Make tools available by MCP checkbox"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2541: Verify Make tools available by MCP checkbox

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify "Make tools available by MCP" checkbox functions correctly

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is on toolkit configuration page

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Locate "Make tools available by MCP" checkbox | Checkbox is available and clickable |
| 2 | Check the checkbox | State persists after save |
| 3 | Save toolkit | MCP availability is configured |
| 4 | Re-open toolkit | Step completes successfully |
| 5 | Verify checkbox state persists | Step completes successfully |

## Expected Final State

Checkbox is available and clickable

## Pass/Fail Criteria

**Pass:**
- Checkbox is available and clickable
- State persists after save
- MCP availability is configured

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
