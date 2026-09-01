---
id: ELITEA-3019
title: "GitLab get_merge_request (SDK) – assignees/reviewers Always Present, Unlike list_merge_requests' Opt-In include_details"
priority: medium
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, get-merge-request, issue:6212, new]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3019: GitLab get_merge_request (SDK) – assignees/reviewers Always Present, Unlike list_merge_requests' Opt-In include_details

**Module:** Gitlab · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm the asymmetry between the two tools: `get_merge_request` internally calls `_normalize_mr(mr, include_details=True)` unconditionally (there is no `include_details` parameter on `GetMergeRequestModel` at all), so `assignees`/`reviewers` should be present on **every** `get_merge_request` call — unlike `list_merge_requests`, where `include_details` is an explicit per-call opt-in ([[ELITEA-3007]]). This test exists to verify actual behavior matches the code and flag it if it doesn't, since it wasn't explicitly asserted in prior exploratory runs.

---

## Preconditions

- GitLab toolkit configured against a repository with at least one MR (with and without actual assignees, if possible).

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `get_merge_request` (SDK) |
| Arguments | `pr_number=<valid IID>`, no other flags set |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `get_merge_request` with only `pr_number` set (no `include_details`-equivalent flag exists to omit) | Response includes `assignees` and `reviewers` keys (possibly empty arrays) |
| 2 | Compare against [[ELITEA-3007]]'s default `list_merge_requests` call (same fields, no `include_details`) | `list_merge_requests` omits these fields by default; `get_merge_request` includes them always — confirming the asymmetry |

---

## Expected Final State

The asymmetry is confirmed as matching the code's actual behavior (or, if it does not match, filed as a discrepancy against the read implementation).

---

## Pass/Fail Criteria

**Pass:** `get_merge_request` always includes `assignees`/`reviewers`, confirming the intentional (if asymmetric) design.
**Fail:** `get_merge_request` omits these fields by default, contradicting the hardcoded `include_details=True` in the code — would indicate either the code was misread or has since changed.
