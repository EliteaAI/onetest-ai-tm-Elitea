---
id: ELITEA-3010
title: "GitLab list_merge_requests (SDK) – Negative/Edge Cases Return Empty List Gracefully"
priority: high
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, list-merge-requests, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3010: GitLab list_merge_requests (SDK) – Negative/Edge Cases Return Empty List Gracefully

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify that filters with no matches (nonexistent author, nonexistent branch) and an out-of-range `page` all return an empty list with no error, rather than raising an exception.

---

## Preconditions

- GitLab toolkit configured against a repository with a known, finite MR count.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `list_merge_requests` (SDK) |
| Calls | `author_username="does-not-exist"`; `source_branch="does-not-exist"`; `page=<beyond last page>` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with a nonexistent `author_username` | Returns `[]`, no error |
| 2 | Call with a nonexistent `source_branch` | Returns `[]`, no error |
| 3 | Call with `page` set beyond the last available page | Returns `[]`, no error |

---

## Expected Final State

All three no-match scenarios degrade gracefully to an empty list.

---

## Pass/Fail Criteria

**Pass:** All three cases return `[]` with no exception raised.
**Fail:** Any case raises an unhandled error, or returns a non-empty/malformed result.
