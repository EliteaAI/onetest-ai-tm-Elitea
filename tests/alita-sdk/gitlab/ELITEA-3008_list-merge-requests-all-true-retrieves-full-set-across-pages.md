---
id: ELITEA-3008
title: "GitLab list_merge_requests (SDK) – all=True Retrieves Full Set Across Pages"
priority: high
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, list-merge-requests, pagination, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3008: GitLab list_merge_requests (SDK) – all=True Retrieves Full Set Across Pages

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify `all=True` bypasses `page`/`per_page` and retrieves the complete result set across multiple GitLab-internal pages, with no truncation or duplication.

---

## Preconditions

- GitLab toolkit configured against a repository with more MRs than a single `per_page` page.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `list_merge_requests` (SDK) |
| Arguments | `all=True, per_page=5` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `all=True, per_page=5` | Returns the full set of matching MRs, more than 5 items if more than 5 exist |
| 2 | Compare the count against a known total (e.g. via `state="all"` without pagination limits, or the repository's UI MR count) | Counts match; no duplicate or missing IDs |

---

## Expected Final State

`all=True` correctly overrides per-page limits to return the complete result set.

---

## Pass/Fail Criteria

**Pass:** Full result set retrieved, no duplicates, no gaps, matches the known total.
**Fail:** Result is truncated to one page's worth, contains duplicates, or times out/errors.
