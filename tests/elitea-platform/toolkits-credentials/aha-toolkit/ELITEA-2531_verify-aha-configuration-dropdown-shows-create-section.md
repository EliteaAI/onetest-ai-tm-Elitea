---
id: ELITEA-2531
title: "Verify Aha Configuration dropdown shows CREATE section"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2531: Verify Aha Configuration dropdown shows CREATE section

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify Aha Configuration dropdown shows CREATE section at top

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is on toolkit configuration page

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Aha Configuration dropdown | CREATE section is first section in dropdown |
| 2 | Observe dropdown structure | Section is clearly labeled |
| 3 | Verify CREATE section is at top | Contains "New private" and "New project" options |
| 4 | Verify it contains credential creation options | Step completes successfully |

## Expected Final State

CREATE section is first section in dropdown

## Pass/Fail Criteria

**Pass:**
- CREATE section is first section in dropdown
- Section is clearly labeled
- Contains "New private" and "New project" options

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
