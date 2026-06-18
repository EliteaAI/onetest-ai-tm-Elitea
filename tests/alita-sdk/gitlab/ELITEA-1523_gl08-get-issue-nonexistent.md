---
id: ELITEA-1523
title: "GL08 - Get Issue (Nonexistent)"
priority: high
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [error-handling, get_issue, negative, gitlab, issues]
requirements: []
---
# ELITEA-1523: GL08 - Get Issue (Nonexistent)

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Test get_issue error handling when an issue ID that does not exist is requested, verifying graceful error response without unhandled exceptions.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
NEGATIVE test — issue IID used does not exist in the repository

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
Non-existent issue IID: 999999

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit and set GITLAB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Use a non-existent issue IID (e.g., 999999) | Invalid IID prepared for NEGATIVE test |
| 3 | Invoke get_issue with the non-existent IID | API request sent with invalid IID |
| 4 | Validate response contains an error message (404 not found or issue does not exist) | Error message returned, not a valid issue object |
| 5 | Confirm no Python exception or stack trace is raised | Tool exits cleanly with error handled |

## Expected Final State

Tool exits cleanly with error handled

## Pass/Fail Criteria

get_issue returns error or empty result for non-existent IID
Error message indicates not found (404) or issue does not exist
No Python stack trace raised
Tool exits cleanly
