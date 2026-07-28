---
id: ELITEA-2514
title: "Verify selected credential persists in toolkit configuration"
priority: critical
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2514: Verify selected credential persists in toolkit configuration

**Module:** Toolkits · **Priority:** Critical · **Type:** Functional

**Objective:** Verify selected credential persists in toolkit configuration after selection

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User has saved Aha! credentials
- User is configuring Aha! toolkit

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open New Aha! Toolkit configuration page | Selected credential persists in configuration |
| 2 | Select credential from Aha Configuration dropdown | Credential value does not reset or change |
| 3 | Enter Toolkit Name | Step completes successfully |
| 4 | Select some tools | Step completes successfully |
| 5 | Observe that selected credential remains in field | Step completes successfully |

## Expected Final State

Selected credential persists in configuration

## Pass/Fail Criteria

**Pass:**
- Selected credential persists in configuration
- Credential value does not reset or change

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
