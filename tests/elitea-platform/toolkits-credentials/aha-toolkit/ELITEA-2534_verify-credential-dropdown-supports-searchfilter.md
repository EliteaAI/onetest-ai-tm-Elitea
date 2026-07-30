---
id: ELITEA-2534
title: "Verify credential dropdown supports search/filter"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2534: Verify credential dropdown supports search/filter

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify credential dropdown supports search/filter functionality

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User has multiple saved credentials

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Aha Configuration dropdown | Search/filter field is available |
| 2 | Locate search/filter field if present | Results filter as user types |
| 3 | Type partial credential name | Matching credentials remain visible |
| 4 | Observe filtered results | Step completes successfully |

## Expected Final State

Search/filter field is available

## Pass/Fail Criteria

**Pass:**
- Search/filter field is available
- Results filter as user types
- Matching credentials remain visible

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
