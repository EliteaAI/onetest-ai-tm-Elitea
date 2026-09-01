---
id: ELITEA-3002
title: "GitLab list_merge_requests (SDK) – updated_after/updated_before 1-Month Window"
priority: medium
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, list-merge-requests, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3002: GitLab list_merge_requests (SDK) – updated_after/updated_before 1-Month Window

**Module:** Gitlab · **Priority:** Medium · **Type:** Functional

**Objective:** Verify `updated_after`/`updated_before` filter on `updated_at`, distinct from `created_after`/`created_before`.

---

## Preconditions

- GitLab toolkit configured against a repository with at least one MR updated (e.g. commented on, rebased) more recently than it was created.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `list_merge_requests` (SDK) |
| Arguments | `updated_after`/`updated_before` spanning 1 month |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with a 1-month `updated_after`/`updated_before` window | Returns MRs whose `updated_at` falls in the window |
| 2 | Confirm at least one returned MR has `created_at` outside the window but `updated_at` inside it | Confirms the filter is keyed on `updated_at`, not `created_at` |

---

## Expected Final State

`updated_after`/`updated_before` filter correctly on the update timestamp.

---

## Pass/Fail Criteria

**Pass:** Matches are based on `updated_at`; an MR created outside but updated inside the window is included.
**Fail:** Filter silently behaves like `created_after`/`created_before`, or excludes a correctly-matching MR.
