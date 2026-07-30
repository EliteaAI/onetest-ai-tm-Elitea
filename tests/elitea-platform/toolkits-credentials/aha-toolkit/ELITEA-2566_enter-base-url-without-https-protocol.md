---
id: ELITEA-2566
title: "Enter Base URL without https protocol"
priority: medium
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2566: Enter Base URL without https protocol

**Module:** Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify system auto-corrects or displays validation error for URL without protocol

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is creating Aha! credential

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open credential form | System auto-corrects to https://subdomain.aha.io OR |
| 2 | Enter Display Name | Validation error displays indicating proper format |
| 3 | Enter Base URL without protocol: subdomain.aha.io | Step completes successfully |
| 4 | Observe system behavior | Step completes successfully |

## Expected Final State

System auto-corrects to https://subdomain.aha.io OR

## Pass/Fail Criteria

**Pass:**
- System auto-corrects to https://subdomain.aha.io OR
- Validation error displays indicating proper format

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
