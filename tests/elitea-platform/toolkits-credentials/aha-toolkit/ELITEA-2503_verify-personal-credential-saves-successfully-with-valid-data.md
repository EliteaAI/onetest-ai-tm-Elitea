---
id: ELITEA-2503
title: "Verify personal credential saves successfully with valid data"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2503: Verify personal credential saves successfully with valid data

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify personal Aha! credential saves successfully when all required fields are filled with valid data

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
| 1 | Open New Aha! Credential form (private/personal scope) | All fields are populated correctly |
| 2 | Enter Display Name: "Test Personal Credential" | Success message displays |
| 3 | Verify ID is auto-filled | Credential is saved and appears in credential list |
| 4 | Enter Base URL: https://test-subdomain.aha.io | Step completes successfully |
| 5 | Enter valid API Key | Step completes successfully |
| 6 | Click Save button | Step completes successfully |
| 7 | Observe save operation result | Step completes successfully |

## Expected Final State

All fields are populated correctly

## Pass/Fail Criteria

**Pass:**
- All fields are populated correctly
- Success message displays
- Credential is saved and appears in credential list

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
