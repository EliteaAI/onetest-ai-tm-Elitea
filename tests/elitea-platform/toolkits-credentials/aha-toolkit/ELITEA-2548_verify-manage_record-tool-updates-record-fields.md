---
id: ELITEA-2548
title: "Verify manage_record tool updates record fields"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2548: Verify manage_record tool updates record fields

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify manage_record tool successfully updates record fields

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit is configured with manage_record tool
- Valid record ID is available

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select manage_record tool | Tool executes successfully |
| 2 | Provide record ID and fields to update | Record fields are updated in Aha! |
| 3 | Click RUN TOOL | Response confirms update |
| 4 | Verify success response | Step completes successfully |
| 5 | Check record in Aha! to confirm updates | Step completes successfully |

## Expected Final State

Tool executes successfully

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- Record fields are updated in Aha!
- Response confirms update

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
