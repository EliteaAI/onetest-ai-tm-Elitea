---
id: ELITEA-3004
title: "GitLab list_merge_requests (SDK) – author_username Filter"
priority: medium
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, list-merge-requests, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3004: GitLab list_merge_requests (SDK) – author_username Filter

**Module:** Gitlab · **Priority:** Medium · **Type:** Functional

**Objective:** Verify `author_username` correctly scopes results to MRs authored by the given GitLab user.

---

## Preconditions

- GitLab toolkit configured against a repository with MRs from more than one author, including a known bot/service account (e.g. `ghost1`).

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `list_merge_requests` (SDK) |
| Arguments | `author_username="ghost1"` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `author_username="ghost1"` | Returns only MRs authored by `ghost1` |
| 2 | Confirm no MR from a different author is included | Filtering is exact |

---

## Expected Final State

`author_username` correctly scopes results to the specified author.

---

## Pass/Fail Criteria

**Pass:** Only MRs by the specified author are returned.
**Fail:** MRs from other authors are included, or a matching MR is omitted.
