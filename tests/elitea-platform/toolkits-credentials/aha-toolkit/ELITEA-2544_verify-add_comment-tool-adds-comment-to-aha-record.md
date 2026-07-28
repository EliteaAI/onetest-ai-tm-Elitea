---
id: ELITEA-2544
title: "Verify add_comment tool adds comment to Aha! record"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2544: Verify add_comment tool adds comment to Aha! record

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify add_comment tool successfully adds comment to Aha! record

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit is configured with add_comment tool enabled
- Valid record ID is available

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select add_comment tool | Tool executes successfully |
| 2 | Provide record ID and comment text | Comment is added to specified record in Aha! |
| 3 | Click RUN TOOL | Success response is returned |
| 4 | Verify success response | Step completes successfully |
| 5 | Check Aha! platform to confirm comment was added | Step completes successfully |

## Expected Final State

Tool executes successfully

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- Comment is added to specified record in Aha!
- Success response is returned

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
