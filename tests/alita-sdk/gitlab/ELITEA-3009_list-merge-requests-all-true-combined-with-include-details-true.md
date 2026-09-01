---
id: ELITEA-3009
title: "GitLab list_merge_requests (SDK) – all=True Combined With include_details=True"
priority: medium
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, list-merge-requests, pagination, issue:6212, new]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3009: GitLab list_merge_requests (SDK) – all=True Combined With include_details=True

**Module:** Gitlab · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the combination of `all=True` and `include_details=True` — which triggers per-item assignee/reviewer normalization across every page of results — completes correctly without truncation, excessive latency, or timeout, on a repository with a non-trivial MR count.

---

## Preconditions

- GitLab toolkit configured against a repository with enough MRs to span multiple GitLab-internal pages (ideally 20+).

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `list_merge_requests` (SDK) |
| Arguments | `all=True, include_details=True` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `all=True, include_details=True` and record wall-clock time | Call completes within a reasonable time (no timeout), returns the full result set |
| 2 | Confirm every returned item includes `assignees`/`reviewers` | Details are present on every item, not just the first page |

---

## Expected Final State

The combination of full-pagination and per-item detail enrichment works correctly at scale.

---

## Pass/Fail Criteria

**Pass:** Full set returned with details on every item, no timeout, no truncation.
**Fail:** Call times out, truncates results, or omits details on later-page items.
