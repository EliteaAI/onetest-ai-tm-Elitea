---
id: ELITEA-3000
title: "GitLab list_merge_requests (SDK) – page/per_page Returns Exact Count, Newest-First"
priority: high
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, list-merge-requests, pagination, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3000: GitLab list_merge_requests (SDK) – page/per_page Returns Exact Count, Newest-First

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify `page`/`per_page` are forwarded correctly to the GitLab API, returning exactly the requested page size in newest-first order.

---

## Preconditions

- GitLab toolkit configured against a repository with more MRs than one page (`per_page`).

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `list_merge_requests` (SDK) |
| Arguments | `page=1, per_page=5` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `page=1, per_page=5` | Returns exactly 5 items |
| 2 | Inspect ordering by creation/update date | Items are ordered newest-first |

---

## Expected Final State

Pagination parameters are honored exactly, with a stable default ordering.

---

## Pass/Fail Criteria

**Pass:** Exactly 5 items returned, newest-first.
**Fail:** Wrong item count returned, or ordering is not newest-first.
