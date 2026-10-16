---
id: ELITEA-3909
title: "Verify API Key field with Secret/Password toggle"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-3909: Verify API Key field with Secret/Password toggle

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify API Key field is required and has Secret/Password toggle button

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
| 1 | Open New Aha! Credential form | Toggle button is present next to API Key field |
| 2 | Locate API Key field | API Key appears as masked characters by default |
| 3 | Verify Secret/Password toggle button is present | Step completes successfully |
| 4 | Enter API Key value in the field | Step completes successfully |
| 5 | Observe that API Key is masked by default | Step completes successfully |

## Expected Final State

Toggle button is present next to API Key field

## Pass/Fail Criteria

**Pass:**
- Toggle button is present next to API Key field
- API Key appears as masked characters by default

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
