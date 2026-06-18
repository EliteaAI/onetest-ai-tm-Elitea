---
id: ELITEA-1500
title: "GH04 - Commits Workflow"
priority: high
type: functional
module: github
status: ready
execution_type: automated
tags: [get_commits_diff, get_commits, commits, github]
requirements: []
---
# ELITEA-1500: GH04 - Commits Workflow

**Module:** Github · **Priority:** High · **Type:** Functional

**Objective:** Test commit operations: retrieve commit history with get_commits, then use get_commits_diff to compare two adjacent commits and verify diff content.

## Preconditions

GitHub toolkit is configured and authenticated
GITHUB_TOOLKIT_NAME env var is set
Target repository has at least two commits in history

## Test Data

GITHUB_TOOLKIT_NAME: configured GitHub toolkit name
GITHUB_REPO: target repository with at least 2 commits
Branch: main
Commit SHAs extracted dynamically from get_commits response

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitHub toolkit and set GITHUB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Invoke get_commits to retrieve commit history from the main branch | List of commits returned with at least two entries |
| 3 | Extract SHA values for two adjacent commits from the response | Two commit SHAs available for comparison |
| 4 | Invoke get_commits_diff with the two extracted commit SHAs | Diff returned showing changes between the two commits |
| 5 | Validate diff contains file change information (files added/modified/deleted) | Diff output contains at least one file entry with change details |

## Expected Final State

Diff output contains at least one file entry with change details

## Pass/Fail Criteria

get_commits returns list with at least two commits
Each commit has SHA and message
get_commits_diff returns diff for two commit SHAs
Diff contains file change information
Both tools complete without error
