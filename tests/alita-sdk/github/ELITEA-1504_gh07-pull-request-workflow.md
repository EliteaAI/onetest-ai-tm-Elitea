---
id: ELITEA-1504
title: "GH07 - Pull Request Workflow"
priority: critical
type: functional
module: github
status: ready
execution_type: automated
tags: [create_pull_request, get_pull_request, pull-requests, workflow, github, smoke]
requirements: []
---
# ELITEA-1504: GH07 - Pull Request Workflow

**Module:** Github · **Priority:** Critical · **Type:** Functional

**Objective:** Test full PR lifecycle: create branch, set active branch, add a file, create pull request, get PR details, list PR diffs, then close the PR and clean up.

## Preconditions

GitHub toolkit is configured and authenticated
GITHUB_TOOLKIT_NAME env var is set
Write access to target repository (branch creation, file creation, PR creation)
Token has repo scope

## Test Data

GITHUB_TOOLKIT_NAME: configured GitHub toolkit name
GITHUB_REPO: target repository with write access and PR creation enabled
Branch name: test/gh07-pr-\u003ctimestamp\u003e
File path: test/gh07_pr_test.txt
File content: "PR workflow test file — GH07"
PR title: "GH07 Automated PR Test"
PR body: "This PR will be closed automatically after validation."
Base branch: main

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitHub toolkit with write access and set GITHUB_TOOLKIT_NAME | Toolkit authenticated with write permissions |
| 2 | Invoke create_branch with unique branch name (e.g., test/gh07-pr-<timestamp>) | Branch created successfully |
| 3 | Invoke set_active_branch to switch to the new branch | Active branch set to new branch |
| 4 | Invoke create_file to add a test file on the branch | File created on the branch |
| 5 | Invoke create_pull_request with title, body, base=main, and head=new branch | PR created successfully with valid PR number returned |
| 6 | Invoke get_pull_request with the PR number to retrieve details | PR details returned with title, state=open, and base/head refs |
| 7 | Invoke list_pull_request_diffs with the PR number | Diff list returned showing the file added in step 4 |
| 8 | Invoke update_issue with the PR number and state=closed to close the PR | PR closed successfully |
| 9 | Verify PR is closed by calling get_pull_request and checking state=closed | PR state confirmed as closed |

## Expected Final State

PR state confirmed as closed

## Pass/Fail Criteria

create_branch returns valid branch name
create_file adds file to branch
create_pull_request returns valid PR number
get_pull_request returns PR with title, state, and base/head refs
list_pull_request_diffs returns file change diffs
update_issue closes the PR
All tools complete without error throughout workflow
