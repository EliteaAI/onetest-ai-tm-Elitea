---
id: ELITEA-2558
title: "Test connection with unreachable Base URL"
priority: high
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2558: Test connection with unreachable Base URL

**Module:** Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify timeout error displays with appropriate message for unreachable URL

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is creating Aha! credential

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enter Display Name | Connection attempt times out |
| 2 | Enter unreachable Base URL (e.g., https://nonexistent-subdomain-12345.aha.io) | Timeout error message displays |
| 3 | Enter valid API Key | Message indicates URL is unreachable |
| 4 | Click Test connection | Step completes successfully |
| 5 | Wait for timeout | Step completes successfully |

## Expected Final State

Connection attempt times out

## Pass/Fail Criteria

**Pass:**
- Connection attempt times out
- Timeout error message displays
- Message indicates URL is unreachable

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
