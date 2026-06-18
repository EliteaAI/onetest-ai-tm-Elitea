---
id: ELITEA-1521
title: "GL07 - Get Issue (Happy Path)"
priority: high
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [get_issue, gitlab, issues, smoke]
requirements: []
---
# ELITEA-1521: GL07 - Get Issue (Happy Path)

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify get_issue retrieves a known existing GitLab issue by ID, returning its title, description, state, and author metadata.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
GITLAB_ISSUE_IID env var set to a known existing issue IID

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
GITLAB_ISSUE_IID: known existing issue IID (e.g., 1)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit and set GITLAB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Set GITLAB_ISSUE_IID to a known existing issue IID | Issue IID ready |
| 3 | Invoke get_issue with the known issue IID | API request sent to GitLab issues endpoint |
| 4 | Validate response contains the issue object with iid matching the requested value | Correct issue returned |
| 5 | Verify issue has title, description, state, and author fields | Issue metadata is complete and properly structured |

## Expected Final State

Issue metadata is complete and properly structured

## Pass/Fail Criteria

get_issue returns issue object without error
Issue has iid, title, state, and author fields
Issue IID matches the queried IID
Tool completes without error
