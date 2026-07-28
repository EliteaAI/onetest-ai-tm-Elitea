---
id: ELITEA-2527
title: "Edit existing personal credential"
priority: high
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2527: Edit existing personal credential

**Module:** Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify user can edit existing personal credential (Display Name or Base URL)

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User has at least one personal Aha! credential

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials page | Credential opens for editing |
| 2 | Locate existing personal credential | Changes save successfully |
| 3 | Click edit/modify option | Updated values display correctly |
| 4 | Change Display Name from "Old Name" to "Updated Name" | Step completes successfully |
| 5 | Change Base URL if needed | Step completes successfully |
| 6 | Click Save | Step completes successfully |
| 7 | Verify changes persist | Step completes successfully |

## Expected Final State

Credential opens for editing

## Pass/Fail Criteria

**Pass:**
- Credential opens for editing
- Changes save successfully
- Updated values display correctly

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
