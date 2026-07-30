---
id: ELITEA-2563
title: "Attempt to create credential with empty Display Name"
priority: medium
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2563: Attempt to create credential with empty Display Name

**Module:** Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify inline validation error displays for empty Display Name

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
| 2 | Leave Display Name empty | Error message indicates Display Name is required |
| 3 | Click into Base URL field (trigger blur event) | Step completes successfully |
| 4 | Observe validation | Step completes successfully |

## Expected Final State

Inline validation error displays

## Pass/Fail Criteria

**Pass:**
- Inline validation error displays
- Error message indicates Display Name is required

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
