---
id: ELITEA-2569
title: "Toggle API Key visibility"
priority: medium
type: security
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2569: Toggle API Key visibility

**Module:** Credentials · **Priority:** Medium · **Type:** Security

**Objective:** Verify API Key becomes visible when toggle button is clicked

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User has entered API Key value

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enter API Key (masked by default) | First click reveals API Key in plain text |
| 2 | Click Secret/Password toggle button | Second click re-masks API Key |
| 3 | Observe API Key field | Step completes successfully |
| 4 | Click toggle again | Step completes successfully |
| 5 | Observe API Key field | Step completes successfully |

## Expected Final State

First click reveals API Key in plain text

## Pass/Fail Criteria

**Pass:**
- First click reveals API Key in plain text
- Second click re-masks API Key

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
