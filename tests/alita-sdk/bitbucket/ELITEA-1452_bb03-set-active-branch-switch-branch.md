---
id: ELITEA-1452
title: "BB03 - Set Active Branch - Switch Branch"
priority: high
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [set_active_branch, bitbucket, branch, smoke]
requirements: []
---
# ELITEA-1452: BB03 - Set Active Branch - Switch Branch

**Module:** Bitbucket · **Priority:** High · **Type:** Functional

**Objective:** Verify the Bitbucket 'set_active_branch' tool successfully switches to an existing branch. Tests that a pre-created test branch with a unique marker file is switched to, and the marker file becomes visible after switching, proving the branch switch worked correctly.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
Pre-created test branch with a unique marker file exists
Marker file does NOT exist on base branch

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
Pre-created test branch: must contain a unique marker file not on base branch
Marker file path: known file unique to the test branch

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call list_files on current (base) branch to check for presence of unique marker file | Marker file is NOT present in the base branch file listing |
| 2 | Call set_active_branch to switch to the pre-created test branch that contains the marker file | Branch switch returns success response |
| 3 | Call list_files on the now-active test branch to check file listings | Marker file IS visible in the file list after switching to test branch |
| 4 | LLM validates: marker was absent before switch, present after switch, proving branch switch worked correctly | Validation confirms set_active_branch successfully changed active branch |
| 5 | Call set_active_branch to switch back to base branch (cleanup) | Active branch restored to base branch |

## Expected Final State

Active branch restored to base branch

## Pass/Fail Criteria

PASS: Marker file absent before switch, present after switch to test branch, set_active_branch returns success
FAIL: Marker file visible on base branch (not isolated), marker missing after switch, branch switch failed
