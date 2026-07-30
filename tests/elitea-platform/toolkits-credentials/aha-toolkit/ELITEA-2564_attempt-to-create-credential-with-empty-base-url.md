---
id: ELITEA-2564
title: "Attempt to create credential with empty Base URL"
priority: medium
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2564: Attempt to create credential with empty Base URL

**Module:** Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify inline validation error displays for empty Base URL

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is creating Aha! credential

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open credential form | Inline validation error displays |
| 2 | Enter Display Name | Error indicates Base URL is required |
| 3 | Leave Base URL empty | Step completes successfully |
| 4 | Click into API Key field | Step completes successfully |
| 5 | Observe validation | Step completes successfully |

## Expected Final State

Inline validation error displays

## Pass/Fail Criteria

**Pass:**
- Inline validation error displays
- Error indicates Base URL is required

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
