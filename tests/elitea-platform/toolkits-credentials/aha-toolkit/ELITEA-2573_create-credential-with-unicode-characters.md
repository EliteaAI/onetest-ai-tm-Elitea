---
id: ELITEA-2573
title: "Create credential with Unicode characters"
priority: medium
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2573: Create credential with Unicode characters

**Module:** Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify Unicode characters render correctly in Display Name

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is creating Aha! credential

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/
- Unicode test string: "Aha! 测试 Тест"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open credential form | Unicode characters are accepted |
| 2 | Enter Display Name with Unicode: "Aha! 测试 Тест" | Characters display correctly |
| 3 | Fill other required fields | No encoding issues |
| 4 | Save credential | Credential saves successfully |
| 5 | Verify Display Name renders correctly | Unicode characters render properly |

## Expected Final State

Unicode characters are accepted and display correctly with no encoding issues.

## Pass/Fail Criteria

**Pass:**
- Unicode characters are accepted
- Characters display correctly
- No encoding issues

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
