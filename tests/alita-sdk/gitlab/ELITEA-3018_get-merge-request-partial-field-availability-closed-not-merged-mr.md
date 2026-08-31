---
id: ELITEA-3018
title: "GitLab get_merge_request (SDK) – Partial Field Availability on a Closed-Not-Merged MR"
priority: medium
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, get-merge-request, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3018: GitLab get_merge_request (SDK) – Partial Field Availability on a Closed-Not-Merged MR

**Module:** Gitlab · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that on an old MR that was closed without being merged, fields specific to a merge event (`merged_at`, `merge_user`) correctly report as absent/`None` while merge-independent fields (e.g. `closed_at`) are still populated — confirming `_normalize_mr`'s defensive field handling doesn't fail on a partially-populated MR.

---

## Preconditions

- GitLab toolkit configured against a repository containing at least one old MR that was closed without merging (e.g. IID `1`).

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `get_merge_request` (SDK) |
| Arguments | `pr_number=<IID of a closed-not-merged MR>` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `get_merge_request` for the closed-not-merged MR | Call succeeds, no error |
| 2 | Inspect `merged_at` and `merge_user` | Both are `None`/absent, not an error or a garbage value |
| 3 | Inspect `closed_at` | Populated with the actual close timestamp |

---

## Expected Final State

Merge-specific fields correctly reflect that no merge occurred, without failing the call.

---

## Pass/Fail Criteria

**Pass:** `merged_at`/`merge_user` are `None`, `closed_at` is populated, no error.
**Fail:** Call errors on the missing merge data, or `merged_at`/`merge_user` contain incorrect/stale values.
