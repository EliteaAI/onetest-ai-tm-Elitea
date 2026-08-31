---
id: ELITEA-3014
title: "GitLab get_merge_request (SDK) – Each Heavy Flag Individually Adds Only Its Own Field"
priority: high
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, get-merge-request, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3014: GitLab get_merge_request (SDK) – Each Heavy Flag Individually Adds Only Its Own Field

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify `include_discussions`, `include_approvals`, `include_pipelines`, and `include_commits`, each set individually, add exactly and only their corresponding field to the response.

---

## Preconditions

- GitLab toolkit configured against a repository with at least one MR that has discussions, an approval, a pipeline, and commits (or, absent one of those, confirm the field degrades gracefully rather than erroring — see [[ELITEA-3016]]).

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `get_merge_request` (SDK) |
| Calls | `include_discussions=True`; `include_approvals=True`; `include_pipelines=True`; `include_commits=True` (one flag per call) |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `include_discussions=True` only | Adds `discussions` (a list) and no other heavy field |
| 2 | Call with `include_approvals=True` only | Adds `approvals` (an object with `approved`/`approved_by`) and no other heavy field |
| 3 | Call with `include_pipelines=True` only | Adds `pipeline` and no other heavy field |
| 4 | Call with `include_commits=True` only | Adds `commits` (a list) and no other heavy field |

---

## Expected Final State

Each heavy flag is independently additive with no cross-contamination between fields.

---

## Pass/Fail Criteria

**Pass:** Each flag adds exactly its own field, nothing else.
**Fail:** A flag adds an unrelated field, fails to add its own field, or affects a field it shouldn't.
