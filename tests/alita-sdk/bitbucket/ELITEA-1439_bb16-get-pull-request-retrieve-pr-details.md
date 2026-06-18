---
id: ELITEA-1439
title: "BB16 - Get Pull Request - Retrieve PR Details"
priority: high
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [get_pull_request, pull-request, bitbucket, smoke]
requirements: []
---
# ELITEA-1439: BB16 - Get Pull Request - Retrieve PR Details

**Module:** Bitbucket · **Priority:** High · **Type:** Functional

**Objective:** Verify the Bitbucket 'get_pull_request' tool retrieves PR details. Tests that tool executes without crashing, returns PR information when PR exists, returns appropriate error when PR doesn't exist, and result is properly structured.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
BB_PR_ID env var is set with existing PR ID

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
BB_PR_ID: ID of existing pull request in repository

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call get_pull_request with BB_PR_ID (existing PR ID from environment variable) | PR details returned without errors |
| 2 | LLM validates: response contains PR details (ID, title, status, source/destination branches), data is properly structured, no crashes | Validation confirms get_pull_request retrieves PR details correctly |

## Expected Final State

Validation confirms get_pull_request retrieves PR details correctly

## Pass/Fail Criteria

PASS: get_pull_request returns PR details with ID, title, and status fields properly structured
FAIL: Tool crashes, returns empty response, or returns malformed data structure
