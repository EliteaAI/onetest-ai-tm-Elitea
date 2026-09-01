---
id: ELITEA-3011
title: "GitLab list_merge_requests (SDK) – Output Field Shape Matches Spec, No Diff Content"
priority: high
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, list-merge-requests, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3011: GitLab list_merge_requests (SDK) – Output Field Shape Matches Spec, No Diff Content

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify each item returned by `list_merge_requests` contains exactly the documented compact field set, and never includes diff/patch content.

---

## Preconditions

- GitLab toolkit configured against a repository with at least one MR.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `list_merge_requests` (SDK) |
| Expected fields | `id, iid, title, web_url, state, draft, created_at, updated_at, merged_at, closed_at, source_branch, target_branch, author, merge_user, labels, sha, merge_commit_sha` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `list_merge_requests` and inspect the field set on a returned item | All expected fields are present |
| 2 | Confirm no `diff`/`changes`/patch-content key is present | No diff content leaks |

---

## Expected Final State

Output shape matches the documented spec exactly, with no diff content.

---

## Pass/Fail Criteria

**Pass:** All expected fields present, no diff content.
**Fail:** A documented field is missing/renamed, an undocumented field appears, or diff content is present.
