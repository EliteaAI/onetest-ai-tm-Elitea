---
id: ELITEA-2535
title: "Select credential and verify checkmark indicator"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2535: Select credential and verify checkmark indicator

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify selected credential highlights with checkmark indicator

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User has saved credentials

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Aha Configuration dropdown | Selected credential highlights |
| 2 | Select a credential | Checkmark icon appears next to selected credential |
| 3 | Observe visual indication | Selection persists when dropdown reopens |
| 4 | Re-open dropdown | Step completes successfully |
| 5 | Verify selected credential shows checkmark | Step completes successfully |

## Expected Final State

Selected credential highlights

## Pass/Fail Criteria

**Pass:**
- Selected credential highlights
- Checkmark icon appears next to selected credential
- Selection persists when dropdown reopens

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
