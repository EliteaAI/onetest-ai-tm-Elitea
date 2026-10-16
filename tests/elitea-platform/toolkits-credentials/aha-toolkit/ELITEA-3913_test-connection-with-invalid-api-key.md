---
id: ELITEA-3913
title: "Test connection with invalid API key"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-3913: Test connection with invalid API key

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify "Test connection" displays error with invalid API key

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User logged in to Elitea application
- User has valid Base URL but invalid API Key

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open New Aha! Credential form | Test connection process initiates |
| 2 | Enter Display Name: "Invalid API Key Test" | Error message displays indicating authentication failure |
| 3 | Enter valid Base URL | Step completes successfully |
| 4 | Enter invalid API Key | Step completes successfully |
| 5 | Click "Test connection" button | Step completes successfully |
| 6 | Wait for connection test to complete | Step completes successfully |

## Expected Final State

Test connection process initiates

## Pass/Fail Criteria

**Pass:**
- Test connection process initiates
- Error message displays indicating authentication failure

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
