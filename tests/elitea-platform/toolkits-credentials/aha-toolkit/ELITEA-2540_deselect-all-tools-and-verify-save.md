---
id: ELITEA-2540
title: "Deselect all tools and verify save"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2540: Deselect all tools and verify save

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify toolkit saves with no tools enabled

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is on toolkit configuration page

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Ensure all tool checkboxes are unchecked | Toolkit saves successfully even with no tools selected |
| 2 | Enter Toolkit Name | Warning message may appear but save completes |
| 3 | Select credential | Step completes successfully |
| 4 | Click Save | Step completes successfully |
| 5 | Observe result | Step completes successfully |

## Expected Final State

Toolkit saves successfully even with no tools selected

## Pass/Fail Criteria

**Pass:**
- Toolkit saves successfully even with no tools selected
- Warning message may appear but save completes

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
