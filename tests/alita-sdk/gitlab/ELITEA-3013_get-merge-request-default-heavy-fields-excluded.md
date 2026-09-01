---
id: ELITEA-3013
title: "GitLab get_merge_request (SDK) – Default Call Excludes All Heavy Fields"
priority: high
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, get-merge-request, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3013: GitLab get_merge_request (SDK) – Default Call Excludes All Heavy Fields

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify that a base `get_merge_request` call (no `include_discussions`/`include_approvals`/`include_pipelines`/`include_commits`) omits all four heavy fields from the response.

---

## Preconditions

- GitLab toolkit configured against a repository with at least one MR.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `get_merge_request` (SDK) |
| Arguments | `pr_number=<valid IID>` only |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with only `pr_number` set | Response contains no `discussions`, `approvals`, `pipeline`, or `commits` keys |

---

## Expected Final State

Heavy, opt-in fields are correctly excluded by default.

---

## Pass/Fail Criteria

**Pass:** None of the four heavy-field keys appear in the default response.
**Fail:** Any heavy-field key appears without being explicitly requested.
