---
id: ELITEA-2510
title: "Test connection with valid credentials"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2510: Test connection with valid credentials

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify "Test connection" button successfully validates connection with valid credentials

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User logged in to Elitea application
- User has valid Aha! API credentials

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open New Aha! Credential form | Test connection process initiates |
| 2 | Enter Display Name: "Valid Credential Test" | Success message displays confirming successful connection |
| 3 | Enter valid Base URL | Step completes successfully |
| 4 | Enter valid API Key | Step completes successfully |
| 5 | Click "Test connection" button | Step completes successfully |
| 6 | Wait for connection test to complete | Step completes successfully |

## Expected Final State

Test connection process initiates

## Pass/Fail Criteria

**Pass:**
- Test connection process initiates
- Success message displays confirming successful connection

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
