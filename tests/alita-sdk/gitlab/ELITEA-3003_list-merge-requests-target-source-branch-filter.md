---
id: ELITEA-3003
title: "GitLab list_merge_requests (SDK) – target_branch/source_branch Filter"
priority: medium
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, list-merge-requests, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3003: GitLab list_merge_requests (SDK) – target_branch/source_branch Filter

**Module:** Gitlab · **Priority:** Medium · **Type:** Functional

**Objective:** Verify `target_branch`/`source_branch` filters, used together, correctly narrow results to MRs matching the exact branch combination.

---

## Preconditions

- GitLab toolkit configured against a repository with MRs targeting more than one branch.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `list_merge_requests` (SDK) |
| Arguments | valid `target_branch`/`source_branch` combination known to match a specific MR |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with a valid `target_branch`+`source_branch` combination | Returns only MRs matching both branch filters |
| 2 | Confirm no MR with a different target or source branch is included | Filtering is exact, not partial/substring |

---

## Expected Final State

Branch filters combine correctly to scope results.

---

## Pass/Fail Criteria

**Pass:** Only MRs matching both branch filters are returned.
**Fail:** Unrelated MRs are included, or a correct match is omitted.
