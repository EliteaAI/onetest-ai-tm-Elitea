---
id: ELITEA-1431
title: "BB19 - Add Pull Request Comment - Regular Comment"
priority: medium
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [add_pull_request_comment, pull-request, bitbucket]
requirements: []
---
# ELITEA-1431: BB19 - Add Pull Request Comment - Regular Comment

**Module:** Bitbucket · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Bitbucket 'add_pull_request_comment' tool adds a regular (non-inline) comment. Tests that comment is added when PR exists, returns appropriate error when PR doesn't exist, and comment ID or confirmation is returned.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
BB_PR_ID env var is set with existing PR ID

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
BB_PR_ID: ID of existing open pull request
Comment text: 'Automated test comment - BB19 {timestamp}'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call add_pull_request_comment on BB_PR_ID with a regular comment text (non-inline) | Comment added to PR, response contains comment ID or success confirmation |
| 2 | LLM validates: comment was added successfully, response contains comment ID or confirmation, no crashes | Validation confirms add_pull_request_comment adds regular comments correctly |

## Expected Final State

Validation confirms add_pull_request_comment adds regular comments correctly

## Pass/Fail Criteria

PASS: Comment added to PR, response contains comment ID or confirmation
FAIL: Tool crashes, no comment ID returned, comment not added to PR
