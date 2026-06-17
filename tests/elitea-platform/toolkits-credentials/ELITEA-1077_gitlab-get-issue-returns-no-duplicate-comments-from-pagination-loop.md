---
id: ELITEA-1077
title: "GitLab - get_issue Returns No Duplicate Comments from Pagination Loop"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [r-2.0.2]
requirements: [EliteaAI/elitea_issues#4055]
---
# ELITEA-1077: GitLab - get_issue Returns No Duplicate Comments from Pagination Loop

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the `while len(comments) <= 10` pagination loop in `get_issue` does not produce duplicate comment entries.

**Coverage:**
- Comment count in response matches actual comment count in GitLab (for ≤10 comments)
- No comment body appears more than once in the returned array
- Pagination loop terminates correctly without doubling entries

## Preconditions

- Logged into {{base_url}} (stage environment)
- Test GitLab issue with exactly 3 distinct comments (different bodies and different users)
- GitLab toolkit configured with `get_issue` tool enabled

## Test Data

- Issue: 3 comments with bodies: "Comment A", "Comment B", "Comment C"
- Expected `comments` count: exactly 3

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Toolkit Test Settings for the configured GitLab toolkit | Settings panel loads |
| 2 | Execute `get_issue` with the issue number containing 3 known comments | Tool output displayed |
| 3 | Count the number of elements in the `comments` array | Array has exactly 3 elements |
| 4 | Inspect each element's `body` value | Three distinct values: "Comment A", "Comment B", "Comment C" — no repeats |
| 5 | Verify no two elements share identical body + user combination | All 3 entries are unique |
| 6 | Execute again with the same issue number (second run) | Response is stable — same 3 elements, no accumulation |

## Expected Final State

Response is stable — same 3 elements, no accumulation

## Pass/Fail Criteria

**Pass:**
- `comments` array length equals the actual number of comments (3)
- All comment bodies are distinct — no duplicates
- Repeated execution produces consistent results

**Fail:**
- `comments` array contains 6 or more items (comments doubled due to loop bug)
- Any comment body appears more than once
- Response length differs between two identical consecutive calls
