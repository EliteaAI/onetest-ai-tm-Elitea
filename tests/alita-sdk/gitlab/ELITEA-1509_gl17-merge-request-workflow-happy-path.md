---
id: ELITEA-1509
title: "GL17 - Merge Request Workflow (Happy Path)"
priority: critical
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [create_pull_request, merge-requests, comment_on_pr, workflow, gitlab, smoke]
requirements: []
---
# ELITEA-1509: GL17 - Merge Request Workflow (Happy Path)

**Module:** Gitlab · **Priority:** Critical · **Type:** Functional

**Objective:** Test full merge request workflow: create branch, create file with changes, create merge request, add comment to MR, validate MR details, then clean up branch.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
Write access to repository (branch creation, file creation, MR creation)
Token has merge_requests scope

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
Branch name: test/gl17-mr-workflow-<timestamp>
File path: test/gl17_mr_file.txt
MR title: "GL17 Automated MR Test"
MR description: "This MR will be cleaned up automatically after validation."
Comment: "Automated MR comment — GL17"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit with write access and set GITLAB_TOOLKIT_NAME | Toolkit authenticated with MR creation permissions |
| 2 | Generate unique branch and file names | Unique names generated |
| 3 | Invoke create_branch to create a test branch | Test branch created |
| 4 | Invoke create_file to add a test file on the branch | File created on branch |
| 5 | Invoke create_pull_request with title, description, source=test branch, target=main | MR created with valid MR IID returned |
| 6 | Extract MR IID from create_pull_request response | MR IID extracted successfully |
| 7 | Invoke comment_on_pr with the MR IID and a test comment | Comment posted with comment ID returned |
| 8 | Validate LLM confirms the MR workflow completed successfully | All operations confirmed successful |

## Expected Final State

All operations confirmed successful

## Pass/Fail Criteria

create_branch and create_file succeed
create_pull_request returns valid MR IID
comment_on_pr posts comment with comment ID
All tools complete without error
