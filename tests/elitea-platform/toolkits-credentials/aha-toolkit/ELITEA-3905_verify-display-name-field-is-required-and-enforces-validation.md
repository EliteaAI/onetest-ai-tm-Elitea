---
id: ELITEA-3905
title: "Verify Display Name field is required and enforces validation"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-3905: Verify Display Name field is required and enforces validation

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Display Name field is required and cannot be left empty when creating Aha! credential

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
| 1 | Open New Aha! Credential form | Validation error message displays indicating Display Name is required |
| 2 | Leave Display Name field empty | Credential is not saved |
| 3 | Fill in all other required fields (ID, Base URL, API Key) | Clear error message appears |
| 4 | Attempt to save credential | Step completes successfully |
| 5 | Observe validation behavior | Step completes successfully |

## Expected Final State

Validation error message displays indicating Display Name is required

## Pass/Fail Criteria

**Pass:**
- Validation error message displays indicating Display Name is required
- Credential is not saved
- Clear error message appears

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
