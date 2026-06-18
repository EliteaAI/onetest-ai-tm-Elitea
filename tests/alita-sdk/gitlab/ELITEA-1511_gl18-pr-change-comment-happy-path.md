---
id: ELITEA-1511
title: "GL18 - PR Change Comment (Happy Path)"
priority: medium
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [create_pr_change_comment, inline-comment, merge-requests, gitlab]
requirements: []
---
# ELITEA-1511: GL18 - PR Change Comment (Happy Path)

**Module:** Gitlab · **Priority:** Medium · **Type:** Functional

**Objective:** Test create_pr_change_comment adds an inline diff comment to a merge request: create branch, create file, create MR, then add an inline comment on a specific line in the diff.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
Write access to repository
Target file and line number for inline comment known

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
Branch name: test/gl18-pr-change-comment-<timestamp>
File path: test/gl18_inline.txt
MR title: "GL18 Inline Comment Test"
Inline comment target: file path gl18_inline.txt, line 1
Comment text: "Inline review comment — GL18"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit with write access and set GITLAB_TOOLKIT_NAME | Toolkit authenticated with MR creation permissions |
| 2 | Generate unique branch and file names | Unique names generated |
| 3 | Invoke create_branch and create a test file with content on the branch | Branch and file created |
| 4 | Invoke create_pull_request to create an MR with the branch changes | MR created with valid MR IID |
| 5 | Extract MR IID from response | MR IID extracted |
| 6 | Invoke create_pr_change_comment with MR IID, file path, line number, and comment text | Inline diff comment posted with comment ID returned |
| 7 | Validate comment references the correct file and line in the MR diff | Inline comment anchored to specified file/line |

## Expected Final State

Inline comment anchored to specified file/line

## Pass/Fail Criteria

create_branch, create_file, and create_pull_request succeed
create_pr_change_comment posts inline comment with comment ID
Comment references correct file and line in the diff
All tools complete without error
