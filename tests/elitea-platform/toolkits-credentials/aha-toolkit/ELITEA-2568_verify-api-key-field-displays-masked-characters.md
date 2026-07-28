---
id: ELITEA-2568
title: "Verify API Key field displays masked characters"
priority: medium
type: security
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2568: Verify API Key field displays masked characters

**Module:** Credentials · **Priority:** Medium · **Type:** Security

**Objective:** Verify API Key field displays masked characters by default

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is creating Aha! credential

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open credential form | API Key appears as dots or asterisks |
| 2 | Enter API Key value | Actual key value is not visible |
| 3 | Observe field display | Step completes successfully |

## Expected Final State

API Key appears as dots or asterisks

## Pass/Fail Criteria

**Pass:**
- API Key appears as dots or asterisks
- Actual key value is not visible

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
