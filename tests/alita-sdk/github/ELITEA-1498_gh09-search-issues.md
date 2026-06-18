---
id: ELITEA-1498
title: "GH09 - Search Issues"
priority: high
type: functional
module: github
status: ready
execution_type: automated
tags: [search_issues, github, issues, smoke]
requirements: []
---
# ELITEA-1498: GH09 - Search Issues

**Module:** Github · **Priority:** High · **Type:** Functional

**Objective:** Verify search_issues tool finds matching issues and pull requests in the repository based on a search query.

## Preconditions

GitHub toolkit is configured and authenticated
GITHUB_TOOLKIT_NAME env var is set
Target repository has at least one issue or PR matching a known search query

## Test Data

GITHUB_TOOLKIT_NAME: configured GitHub toolkit name
GITHUB_REPO: target repository with issues enabled
Search query: a keyword present in at least one existing issue or PR title (e.g., "bug" or "test")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitHub toolkit and set GITHUB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Invoke search_issues with a relevant search query (e.g., a keyword known to exist in issues) | API request sent to GitHub search endpoint |
| 3 | Validate response contains a list of search results | Results list returned (may include issues and PRs) |
| 4 | Verify each result has number, title, and state fields | Search result metadata is complete |
| 5 | Confirm at least one result matches the search query keyword | Search returned relevant results |

## Expected Final State

Search returned relevant results

## Pass/Fail Criteria

search_issues returns a results list
Each result has number, title, and state fields
At least one result matches the search query
Tool completes without error
