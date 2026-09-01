---
id: ELITEA-2998
title: "GitLab list_merge_requests (SDK) – Callable With No Arguments, Returns Compact MR List"
priority: high
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, list-merge-requests, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-2998: GitLab list_merge_requests (SDK) – Callable With No Arguments, Returns Compact MR List

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify `list_merge_requests` is callable with no arguments and returns a compact list of merge request metadata for the configured repository, with no diff content.

---

## Preconditions

- GitLab toolkit is configured with valid credentials against a repository containing a mix of open, closed, and merged MRs.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `list_merge_requests` (SDK) |
| Arguments | none (all defaults) |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `list_merge_requests` with no arguments | Call succeeds, returns a list of MR objects |
| 2 | Inspect each returned item | Each item contains only compact metadata fields; no diff/patch content present |

---

## Expected Final State

A default call returns a usable, compact list of merge requests for the configured repository.

---

## Pass/Fail Criteria

**Pass:** Call succeeds and returns a compact list of MRs with no diff content.
**Fail:** Call errors, returns an empty/malformed result despite MRs existing, or leaks diff content.
