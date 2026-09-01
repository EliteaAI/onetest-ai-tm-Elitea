---
id: ELITEA-2999
title: "GitLab list_merge_requests (SDK) – state Filter (opened/closed/merged/all)"
priority: high
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, list-merge-requests, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-2999: GitLab list_merge_requests (SDK) – state Filter (opened/closed/merged/all)

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify `list_merge_requests`'s `state` parameter correctly filters results to `opened`, `closed`, `merged`, or `all`, including the case where a state has zero matches in the repository.

---

## Preconditions

- GitLab toolkit configured against a repository with a known number of open and closed MRs (a repository with zero merged MRs is acceptable and expected to exercise the empty-result path).

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `list_merge_requests` (SDK) |
| Calls | `state="opened"`, `state="closed"`, `state="merged"`, `state="all"` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `state="opened"` | Returns only open MRs, count matches the known open count |
| 2 | Call with `state="closed"` | Returns only closed MRs |
| 3 | Call with `state="merged"` on a repository with no merged MRs | Returns `[]`, no error |
| 4 | Call with `state="all"` | Returns the union of open+closed(+merged) MRs, no crash |

---

## Expected Final State

`state` filtering behaves correctly for every valid value, including a value with zero matches.

---

## Pass/Fail Criteria

**Pass:** Each `state` value returns the correctly filtered set; a zero-match state returns an empty list without error.
**Fail:** Any `state` value returns an incorrect set, raises an error on zero matches, or `all` omits a state.
