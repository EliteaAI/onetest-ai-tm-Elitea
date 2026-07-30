---
id: ELITEA-2516
title: "Verify toolkit can use either personal or project credential"
priority: critical
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2516: Verify toolkit can use either personal or project credential

**Module:** Toolkits · **Priority:** Critical · **Type:** Functional

**Objective:** Verify toolkit can be configured with either personal or project credential type

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User has both personal and project Aha! credentials
- User is on New Aha! Toolkit configuration page

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create first toolkit using personal credential | Toolkit accepts personal credential |
| 2 | Save toolkit successfully | Toolkit accepts project credential |
| 3 | Create second toolkit using project credential | Both configurations save successfully |
| 4 | Save toolkit successfully | Step completes successfully |
| 5 | Verify both toolkits work correctly | Step completes successfully |

## Expected Final State

Toolkit accepts personal credential

## Pass/Fail Criteria

**Pass:**
- Toolkit accepts personal credential
- Toolkit accepts project credential
- Both configurations save successfully

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
