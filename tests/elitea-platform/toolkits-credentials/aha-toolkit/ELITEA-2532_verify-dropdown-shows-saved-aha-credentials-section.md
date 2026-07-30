---
id: ELITEA-2532
title: "Verify dropdown shows SAVED AHA CREDENTIALS section"
priority: high
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p1]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2532: Verify dropdown shows SAVED AHA CREDENTIALS section

**Module:** Toolkits · **Priority:** High · **Type:** Functional

**Objective:** Verify dropdown shows SAVED AHA CREDENTIALS section below CREATE

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User has at least one saved credential
- User is on toolkit configuration page

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Aha Configuration dropdown | SAVED AHA CREDENTIALS section appears below CREATE |
| 2 | Scroll past CREATE section | Section is clearly labeled |
| 3 | Locate SAVED AHA CREDENTIALS section | Saved credentials are displayed with Display Names |
| 4 | Verify saved credentials are listed | Step completes successfully |

## Expected Final State

SAVED AHA CREDENTIALS section appears below CREATE

## Pass/Fail Criteria

**Pass:**
- SAVED AHA CREDENTIALS section appears below CREATE
- Section is clearly labeled
- Saved credentials are displayed with Display Names

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
