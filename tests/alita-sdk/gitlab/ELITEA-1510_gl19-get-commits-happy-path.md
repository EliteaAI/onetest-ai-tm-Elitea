---
id: ELITEA-1510
title: "GL19 - Get Commits (Happy Path)"
priority: high
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [get_commits, commits, gitlab, smoke]
requirements: []
---
# ELITEA-1510: GL19 - Get Commits (Happy Path)

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify get_commits retrieves the commit history from the repository's default branch, returning a list of commits with SHA, message, and author metadata.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
Target repository has at least one commit

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
Branch: default (main or master)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit and set GITLAB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Invoke get_commits on the repository default branch | API request sent to GitLab commits endpoint |
| 3 | Validate response contains a list of commit objects | Commits list returned with at least one entry |
| 4 | Verify each commit has id (SHA), title or message, and author_name fields | Commit metadata is complete |
| 5 | Confirm at least two commits are returned | Repository has commit history |

## Expected Final State

Repository has commit history

## Pass/Fail Criteria

get_commits returns non-empty list
Each commit has id/sha, title/message, and author_name
Tool completes without error
