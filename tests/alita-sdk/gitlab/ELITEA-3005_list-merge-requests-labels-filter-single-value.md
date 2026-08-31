---
id: ELITEA-3005
title: "GitLab list_merge_requests (SDK) – labels Filter (Single Value)"
priority: medium
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, list-merge-requests, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3005: GitLab list_merge_requests (SDK) – labels Filter (Single Value)

**Module:** Gitlab · **Priority:** Medium · **Type:** Functional

**Objective:** Verify `labels` (a comma-separated string) correctly scopes results to MRs carrying the given label, for a single-label filter.

---

## Preconditions

- GitLab toolkit configured against a repository with at least one MR carrying a known label (e.g. `created-by-agent`) and at least one MR without it.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `list_merge_requests` (SDK) |
| Arguments | `labels="created-by-agent"` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `labels="created-by-agent"` | Returns only MRs carrying that label |
| 2 | Confirm an MR without the label is excluded | Filtering is exact |

---

## Expected Final State

Single-label filtering via the comma-separated `labels` string works correctly.

---

## Pass/Fail Criteria

**Pass:** Only MRs carrying the specified label are returned.
**Fail:** MRs without the label are included, or a labeled MR is omitted.
