---
id: ELITEA-2533
title: "Verify saved credentials display with Display Names"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2533: Verify saved credentials display with Display Names

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify saved credentials display with their Display Names in dropdown

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User has credentials with specific Display Names

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create credential with Display Name "Production Aha" | "Production Aha" appears in dropdown |
| 2 | Create credential with Display Name "Staging Aha" | "Staging Aha" appears in dropdown |
| 3 | Open Aha Configuration dropdown | Display Names are clearly readable |
| 4 | Verify both credentials show their Display Names | Step completes successfully |

## Expected Final State

"Production Aha" appears in dropdown

## Pass/Fail Criteria

**Pass:**
- "Production Aha" appears in dropdown
- "Staging Aha" appears in dropdown
- Display Names are clearly readable

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
