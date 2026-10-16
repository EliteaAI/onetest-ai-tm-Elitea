---
id: ELITEA-3914
title: "Test connection with invalid Base URL format"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-3914: Test connection with invalid Base URL format

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify "Test connection" displays validation error for incorrect URL format

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User logged in to Elitea application

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open New Aha! Credential form | Validation error displays for incorrect URL format |
| 2 | Enter Display Name: "Invalid URL Test" | Clear message indicates proper format required |
| 3 | Enter invalid Base URL format (e.g., "invalid-url" or "http://wrong.com") | Step completes successfully |
| 4 | Enter valid API Key | Step completes successfully |
| 5 | Click "Test connection" button | Step completes successfully |
| 6 | Observe validation behavior | Step completes successfully |

## Expected Final State

Validation error displays for incorrect URL format

## Pass/Fail Criteria

**Pass:**
- Validation error displays for incorrect URL format
- Clear message indicates proper format required

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
