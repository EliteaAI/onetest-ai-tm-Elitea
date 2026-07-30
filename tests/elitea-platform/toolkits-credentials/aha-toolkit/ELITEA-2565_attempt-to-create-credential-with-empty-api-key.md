---
id: ELITEA-2565
title: "Attempt to create credential with empty API Key"
priority: medium
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2565: Attempt to create credential with empty API Key

**Module:** Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify inline validation error displays for empty API Key

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is creating Aha! credential

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open credential form | Validation error displays |
| 2 | Enter Display Name and Base URL | Error indicates API Key is required |
| 3 | Leave API Key empty | Step completes successfully |
| 4 | Attempt to save | Step completes successfully |
| 5 | Observe validation | Step completes successfully |

## Expected Final State

Validation error displays

## Pass/Fail Criteria

**Pass:**
- Validation error displays
- Error indicates API Key is required

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
