---
id: ELITEA-2494
title: "Create new Aha! toolkit from + Toolkit button"
priority: critical
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2494: Create new Aha! toolkit from + Toolkit button

**Module:** Toolkits · **Priority:** Critical · **Type:** Functional

**Objective:** Verify clicking "+ Toolkit" button and selecting Aha! opens the toolkit creation page with pre-selected credential if exists, or empty fields if no credentials exist

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User logged in to Elitea application
- User has access to Toolkits section
- Aha! toolkit is available in Project Management category

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits & Indexes page | Toolkit selection dialog/list appears |
| 2 | Click "+ Toolkit" button | Aha! toolkit is selectable |
| 3 | Select Aha! from the toolkits list | "New Aha! Toolkit" creation page opens without errors |
| 4 | Observe the New Aha! Toolkit creation page that opens | If credentials exist, one is pre-selected; if no credentials exist, field shows empty/placeholder state |
| 5 | Check Aha Configuration dropdown field | Step completes successfully |

## Expected Final State

Toolkit selection dialog/list appears

## Pass/Fail Criteria

**Pass:**
- Toolkit selection dialog/list appears
- Aha! toolkit is selectable
- "New Aha! Toolkit" creation page opens without errors
- If credentials exist, one is pre-selected; if no credentials exist, field shows empty/placeholder state

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
