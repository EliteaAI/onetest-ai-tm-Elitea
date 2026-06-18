---
id: ELITEA-1438
title: "BB17 - Get Pull Request Commits"
priority: medium
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [get_pull_requests_commits, pull-request, bitbucket]
requirements: []
---
# ELITEA-1438: BB17 - Get Pull Request Commits

**Module:** Bitbucket · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Bitbucket 'get_pull_requests_commits' tool retrieves PR commits. Tests that tool executes without crashing, returns commit list when PR exists, returns appropriate error when PR doesn't exist, and commits have expected structure (SHA, message, author).

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
BB_PR_ID env var is set with existing PR ID

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
BB_PR_ID: ID of existing pull request with at least one commit

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call get_pull_requests_commits with BB_PR_ID (existing PR ID from environment variable) | Commit list returned without errors |
| 2 | LLM validates: response contains list of commits, each commit has expected structure (SHA/hash, message, author), at least one commit present | Validation confirms get_pull_requests_commits retrieves commit history correctly for PR |

## Expected Final State

Validation confirms get_pull_requests_commits retrieves commit history correctly for PR

## Pass/Fail Criteria

PASS: Commit list returned with expected structure per commit (SHA/hash, message, author), at least one commit in PR
FAIL: Tool crashes, empty commit list, commits missing required fields
