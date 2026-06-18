---
id: ELITEA-1434
title: "BB18 - Get Pull Request Changes"
priority: medium
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [get_pull_requests_changes, pull-request, bitbucket]
requirements: []
---
# ELITEA-1434: BB18 - Get Pull Request Changes

**Module:** Bitbucket · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Bitbucket 'get_pull_requests_changes' tool retrieves PR file changes. Tests that tool executes without crashing, returns file change list when PR exists, returns appropriate error when PR doesn't exist, and changes show file paths and modification types.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
BB_PR_ID env var is set with existing PR ID

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
BB_PR_ID: ID of existing pull request with file changes

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call get_pull_requests_changes with BB_PR_ID (existing PR ID from environment variable) | File change list returned without errors |
| 2 | LLM validates: response contains list of file changes, each change includes file path and modification type (added/modified/removed), at least one change present | Validation confirms get_pull_requests_changes retrieves file change list correctly for PR |

## Expected Final State

Validation confirms get_pull_requests_changes retrieves file change list correctly for PR

## Pass/Fail Criteria

PASS: File change list returned with file paths and modification types (added/modified/removed)
FAIL: Tool crashes, empty changes list, changes missing file paths or modification types
