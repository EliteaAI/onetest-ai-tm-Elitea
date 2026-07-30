---
id: ELITEA-2572
title: "Create credential with very long Display Name"
priority: medium
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2572: Create credential with very long Display Name

**Module:** Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify field handles long input with truncation or scrolling

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is creating Aha! credential

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open credential form | Field accepts long input |
| 2 | Enter very long Display Name (100+ characters) | UI handles display with truncation or ellipsis |
| 3 | Observe field behavior | Full name visible on hover or in expanded view |
| 4 | Save credential | Credential saves successfully |
| 5 | View credential in dropdown | Display Name shows with appropriate truncation |

## Expected Final State

Field accepts long input and UI handles display with truncation or ellipsis.

## Pass/Fail Criteria

**Pass:**
- Field accepts long input
- UI handles display with truncation or ellipsis
- Full name visible on hover or in expanded view

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
