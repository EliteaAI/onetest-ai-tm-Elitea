---
id: ELITEA-3017
title: "GitLab get_merge_request (SDK) – Nonexistent IID Returns Clean, Structured 404 Error"
priority: high
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, get-merge-request, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3017: GitLab get_merge_request (SDK) – Nonexistent IID Returns Clean, Structured 404 Error

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify calling `get_merge_request` with a nonexistent MR IID returns a clean, structured error (no raw traceback or internal file path), matching the `ToolException(f"Merge request number {pr_number} wasn't found: {e}")` contract in the code.

---

## Preconditions

- GitLab toolkit configured against a repository where the given IID is known not to exist.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `get_merge_request` (SDK) |
| Arguments | `pr_number=99999` (or any IID confirmed not to exist in the repository) |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `pr_number=99999` | Call fails, but with a clean, structured error explaining the MR wasn't found |
| 2 | Inspect the error text | No raw HTTP traceback, no internal file paths/stack frames |

---

## Expected Final State

A nonexistent MR IID produces a clear, caller-facing error with no leaked internals.

---

## Pass/Fail Criteria

**Pass:** Error message clearly states the MR wasn't found, with no traceback/path leakage.
**Fail:** Raw exception/traceback surfaces to the caller, or the call silently returns an empty/incorrect result instead of erroring.
