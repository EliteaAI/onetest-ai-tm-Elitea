---
id: ELITEA-2571
title: "Create credential with special characters in Display Name"
priority: medium
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2571: Create credential with special characters in Display Name

**Module:** Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify credential saves with special characters in Display Name

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is creating Aha! credential

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open credential form | Special characters are accepted |
| 2 | Enter Display Name with special characters: "Prod@#$% & Test" | Credential saves successfully |
| 3 | Fill other required fields | Display Name renders correctly |
| 4 | Save credential | Step completes successfully |
| 5 | Verify Display Name displays correctly | Step completes successfully |

## Expected Final State

Special characters are accepted

## Pass/Fail Criteria

**Pass:**
- Special characters are accepted
- Credential saves successfully
- Display Name renders correctly

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
