---
id: ELITEA-1514
title: "GL15 - Comment on Issue (Happy Path)"
priority: high
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [comment_on_issue, gitlab, issues]
requirements: []
---
# ELITEA-1514: GL15 - Comment on Issue (Happy Path)

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Test comment_on_issue posts a comment to an existing GitLab issue, verifying the comment is created and a comment ID is returned.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
Write access to repository issues
GITLAB_ISSUE_IID env var set to an existing open issue IID

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
GITLAB_ISSUE_IID: existing open issue IID
Comment text: "Automated test comment — GL15 — <timestamp>"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit and set GITLAB_TOOLKIT_NAME | Toolkit authenticated with write permissions for issues |
| 2 | Set GITLAB_ISSUE_IID to an existing open issue IID | Issue IID ready |
| 3 | Generate a unique comment text (with timestamp to avoid duplicates) | Unique comment text prepared |
| 4 | Invoke comment_on_issue with the issue IID and comment text | POST request sent to GitLab notes endpoint |
| 5 | Validate response contains a new comment/note ID | Comment created with ID in response |
| 6 | Verify comment text matches what was submitted | Comment body confirmed |

## Expected Final State

Comment body confirmed

## Pass/Fail Criteria

comment_on_issue returns success response with comment ID
Comment text is present in the response
Tool completes without error
