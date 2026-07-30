---
id: ELITEA-2500
title: "Verify ID field is auto-filled and unique"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2500: Verify ID field is auto-filled and unique

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify ID field is automatically filled with unique value and cannot be duplicated

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User logged in to Elitea application
- New Aha! Credential creation form is open

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open New Aha! Credential form | ID field is auto-filled with unique identifier |
| 2 | Observe ID field without entering any data | System prevents duplicate IDs |
| 3 | Enter Display Name in Display Name field | Step completes successfully |
| 4 | Observe ID field after entering Display Name | Step completes successfully |
| 5 | Verify ID field value is unique | Step completes successfully |

## Expected Final State

ID field is auto-filled with unique identifier

## Pass/Fail Criteria

**Pass:**
- ID field is auto-filled with unique identifier
- System prevents duplicate IDs

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
