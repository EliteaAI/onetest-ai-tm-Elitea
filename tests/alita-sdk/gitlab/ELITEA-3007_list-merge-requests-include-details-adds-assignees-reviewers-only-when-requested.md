---
id: ELITEA-3007
title: "GitLab list_merge_requests (SDK) – include_details Adds assignees/reviewers Only When Requested"
priority: high
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, list-merge-requests, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3007: GitLab list_merge_requests (SDK) – include_details Adds assignees/reviewers Only When Requested

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify `include_details=True` adds `assignees`/`reviewers` fields to each result, and that these fields are absent by default (`include_details` unset/`False`).

---

## Preconditions

- GitLab toolkit configured against a repository with at least one MR.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `list_merge_requests` (SDK) |
| Calls | default (no `include_details`); `include_details=True` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with default arguments | Results omit `assignees`/`reviewers` |
| 2 | Call with `include_details=True` | Results include `assignees`/`reviewers` (may be empty arrays if none assigned), no other unexpected fields added |

---

## Expected Final State

`include_details` is a correctly opt-in per-call flag on `list_merge_requests`.

---

## Pass/Fail Criteria

**Pass:** `assignees`/`reviewers` present only when `include_details=True`, absent by default.
**Fail:** Fields present by default, missing when requested, or unrelated fields change based on this flag.
