---
id: ELITEA-2536
title: "Verify dropdown closes after credential selection"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2536: Verify dropdown closes after credential selection

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify dropdown closes automatically after credential selection

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is on toolkit configuration page

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Aha Configuration dropdown | Dropdown closes after selection |
| 2 | Click on a credential to select | Selected credential appears in field |
| 3 | Observe dropdown behavior | Step completes successfully |

## Expected Final State

Dropdown closes after selection

## Pass/Fail Criteria

**Pass:**
- Dropdown closes after selection
- Selected credential appears in field

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
