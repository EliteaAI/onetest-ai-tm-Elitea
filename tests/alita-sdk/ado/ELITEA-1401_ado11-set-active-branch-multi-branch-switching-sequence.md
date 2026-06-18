---
id: ELITEA-1401
title: "ADO11 - set_active_branch: Multi-branch switching sequence"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1401: ADO11 - set_active_branch: Multi-branch switching sequence

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'set_active_branch' tool can switch between multiple branches.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
Multiple branches exist: 'main', 'EliteaTest', and at least one more branch.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `set_active_branch` tool to switch to branch A (e.g., 'EliteaTest') | First branch switch completes successfully |
| 3 | Call `set_active_branch` tool to switch to branch B (e.g., another test branch) | Second branch switch completes successfully |
| 4 | Call `set_active_branch` tool to switch back to 'main' | Third branch switch completes successfully |
| 5 | Verify all three switch responses confirm success without errors | All responses contain success information and no 'error' or 'failed' |

## Expected Final State

All responses contain success information and no 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
all_switches_succeeded = true
no_error = true
