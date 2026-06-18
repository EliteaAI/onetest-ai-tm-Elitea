---
id: ELITEA-1517
title: "GL14 - Set Active Branch (Happy Path)"
priority: high
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [set_active_branch, branches, gitlab]
requirements: []
---
# ELITEA-1517: GL14 - Set Active Branch (Happy Path)

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Test set_active_branch switches the active working branch: create a test branch, call set_active_branch with the new branch name, verify the switch is confirmed, then clean up.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
Write access to repository

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
Branch name: test/gl14-set-active-<timestamp>

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit and set GITLAB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Generate a unique branch name | Branch name ready |
| 3 | Invoke create_branch to create the test branch | Test branch created |
| 4 | Invoke set_active_branch with the new branch name | Active branch switched to the test branch |
| 5 | Validate response confirms the branch switch (e.g., confirmation message or active branch name) | set_active_branch returns confirmation without error |
| 6 | Invoke delete_branch to clean up the test branch | Test branch deleted |

## Expected Final State

Test branch deleted

## Pass/Fail Criteria

create_branch succeeds
set_active_branch returns confirmation without error
Active branch context updated to new branch
delete_branch succeeds
