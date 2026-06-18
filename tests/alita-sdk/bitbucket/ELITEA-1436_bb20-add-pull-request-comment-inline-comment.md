---
id: ELITEA-1436
title: "BB20 - Add Pull Request Comment - Inline Comment"
priority: medium
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [add_pull_request_comment, pull-request, bitbucket, inline]
requirements: []
---
# ELITEA-1436: BB20 - Add Pull Request Comment - Inline Comment

**Module:** Bitbucket · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Bitbucket 'add_pull_request_comment' tool adds an inline comment to a specific file/line in a PR. Tests that inline comment is added when PR and file exist, returns appropriate error when PR/file doesn't exist, and inline comment format is correctly processed.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
BB_PR_ID env var is set with existing PR ID
PR has file changes to reference for inline comment

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
BB_PR_ID: ID of existing open pull request with file changes
Inline comment target: file path from PR changes, line number from that file
Inline comment text: 'Inline test comment - BB20 {timestamp}'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Build inline comment JSON payload with file path, line number (from), and comment text for the PR file change | Inline comment payload constructed with correct format including file path and line anchor |
| 2 | Call add_pull_request_comment on BB_PR_ID with the inline comment JSON payload | Inline comment added to PR at specified file/line, response contains comment ID or confirmation |
| 3 | LLM validates: inline comment was processed correctly with file and line anchor, response confirms addition, no crashes | Validation confirms add_pull_request_comment handles inline comment format correctly |

## Expected Final State

Validation confirms add_pull_request_comment handles inline comment format correctly

## Pass/Fail Criteria

PASS: Inline comment added with correct format, response contains comment ID, file/line anchor present
FAIL: Tool crashes, inline format not processed, comment not anchored to specified file/line
