---
id: ELITEA-2497
title: "Create new personal Aha! credential with all required fields"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2497: Create new personal Aha! credential with all required fields

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify user can successfully create a new personal Aha! credential by providing all required fields

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User logged in to Elitea application
- User has valid Aha! account credentials (Base URL and API Key)

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials page or open Aha Configuration dropdown in toolkit | New Aha! Credential form opens |
| 2 | Click "New private aha credentials" option | Display Name accepts text input |
| 3 | Enter value in Display Name field (e.g., "Test Aha Credential") | ID field is auto-filled with unique value |
| 4 | Observe ID field behavior | Base URL field accepts valid URL format |
| 5 | Enter Base URL in format https://subdomain.aha.io | API Key field accepts input (displayed as masked) |
| 6 | Enter valid API Key in API Key field | Toggle button is visible next to API Key field |
| 7 | Verify Secret/Password toggle button is present | Credential saves successfully, success message displays |
| 8 | Click "Save" button | Step completes successfully |

## Expected Final State

New Aha! Credential form opens

## Pass/Fail Criteria

**Pass:**
- New Aha! Credential form opens
- Display Name accepts text input
- ID field is auto-filled with unique value
- Base URL field accepts valid URL format
- API Key field accepts input (displayed as masked)
- Toggle button is visible next to API Key field
- Credential saves successfully, success message displays

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
