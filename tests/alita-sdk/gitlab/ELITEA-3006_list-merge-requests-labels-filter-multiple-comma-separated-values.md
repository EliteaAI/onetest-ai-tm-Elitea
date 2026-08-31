---
id: ELITEA-3006
title: "GitLab list_merge_requests (SDK) – labels Filter With Multiple Comma-Separated Values"
priority: medium
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, list-merge-requests, issue:6212, new]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3006: GitLab list_merge_requests (SDK) – labels Filter With Multiple Comma-Separated Values

**Module:** Gitlab · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the AND-vs-OR semantics of `labels` when given multiple comma-separated label names, since this is not documented in the tool's signature and was not exercised by single-label testing ([[ELITEA-3005]]).

---

## Preconditions

- GitLab toolkit configured against a repository with MRs covering all four label combinations: both labels, only label A, only label B, neither.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `list_merge_requests` (SDK) |
| Arguments | `labels="<label-a>,<label-b>"` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `labels="<label-a>,<label-b>"` | Returns a result set |
| 2 | Compare the result set against the known label-combination map | Determine and document whether the tool applies AND (only MRs with both labels) or OR (MRs with either label) semantics |

---

## Expected Final State

The multi-label semantics of `labels` are determined and documented for future reference (this is GitLab's native API behavior — the SDK tool is expected to forward the string as-is).

---

## Pass/Fail Criteria

**Pass:** Result set matches one semantic consistently (either AND or OR) with no partial/inconsistent matches.
**Fail:** Result set is inconsistent with either semantic (e.g. includes an MR with neither label), or the call errors.
