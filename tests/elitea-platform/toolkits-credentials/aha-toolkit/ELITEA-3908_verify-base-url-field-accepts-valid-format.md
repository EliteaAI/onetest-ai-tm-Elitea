---
id: ELITEA-3908
title: "Verify Base URL field accepts valid format"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-3908: Verify Base URL field accepts valid format

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Base URL field is required and accepts valid format

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
| 1 | Open New Aha! Credential form | Base URL field accepts the valid format |
| 2 | Enter valid Display Name and ID | Credential saves successfully with valid Base URL |
| 3 | Enter Base URL in correct format: https://subdomain.aha.io | Step completes successfully |
| 4 | Enter valid API Key | Step completes successfully |
| 5 | Click Save button | Step completes successfully |

## Expected Final State

Base URL field accepts the valid format

## Pass/Fail Criteria

**Pass:**
- Base URL field accepts the valid format
- Credential saves successfully with valid Base URL

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
