---
id: ELITEA-1502
title: "GH05 - List Pull Requests"
priority: high
type: functional
module: github
status: ready
execution_type: automated
tags: [list_open_pull_requests, pull-requests, github, smoke]
requirements: []
---
# ELITEA-1502: GH05 - List Pull Requests

**Module:** Github · **Priority:** High · **Type:** Functional

**Objective:** Verify list_open_pull_requests tool retrieves the PR list from the configured repository with expected PR metadata.

## Preconditions

GitHub toolkit is configured and authenticated
GITHUB_TOOLKIT_NAME env var is set
Target repository exists and is accessible

## Test Data

GITHUB_TOOLKIT_NAME: configured GitHub toolkit name
GITHUB_REPO: target repository

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitHub toolkit and set GITHUB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Invoke list_open_pull_requests on the configured repository | API request sent to GitHub pull requests endpoint |
| 3 | Validate response is a list (may be empty if no open PRs) | PR list returned without error |
| 4 | If PRs are present, verify each PR entry has number, title, and state fields | PR metadata is complete and properly structured |
| 5 | Confirm state of all returned PRs is open | All returned PRs have state=open |

## Expected Final State

All returned PRs have state=open

## Pass/Fail Criteria

list_open_pull_requests returns a list (may be empty if no open PRs)
Each PR object contains number, title, and state fields
Tool completes without error
