---
id: ELITEA-3001
title: "GitLab list_merge_requests (SDK) – created_after/created_before Narrow and Wide Windows"
priority: high
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, list-merge-requests, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3001: GitLab list_merge_requests (SDK) – created_after/created_before Narrow and Wide Windows

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify `created_after`/`created_before` correctly narrow results to MRs created within the given window, for both a narrow (1-day) and a wide (1-month) window, and that results are stable on repeated calls.

---

## Preconditions

- GitLab toolkit configured against a repository with MRs spread across at least a month of creation dates.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `list_merge_requests` (SDK) |
| Calls | `created_after`/`created_before` spanning 1 day; then spanning 1 month |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with a 1-day `created_after`/`created_before` window | Returns only MRs created within that day |
| 2 | Call with a 1-month `created_after`/`created_before` window | Returns only MRs created within that month, superset of step 1's matches |
| 3 | Repeat step 2 in isolation (not as part of a large parallel test batch) at least twice | Both isolated reruns return the identical set of matches |

---

## Expected Final State

Date-window filtering is accurate for both narrow and wide windows and reproducible when run in isolation.

---

## Pass/Fail Criteria

**Pass:** Both windows return the correct, consistent set of matches across isolated reruns.
**Fail:** Either window returns an incorrect set, or isolated reruns of the same window disagree (a real regression, not attributable to concurrent/batched execution).

**Note:** during initial exploratory testing, a single-item result was observed for this filter inside a heavy parallel test batch that did not reproduce on an isolated retest (which returned the correct 5 matches consistently). This is suspected to be a batching/concurrency artifact rather than a filter bug — this test case exists to run the check in isolation and confirm that suspicion, or surface a real regression if it recurs.
