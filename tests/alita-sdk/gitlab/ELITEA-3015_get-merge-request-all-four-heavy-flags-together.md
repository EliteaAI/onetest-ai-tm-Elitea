---
id: ELITEA-3015
title: "GitLab get_merge_request (SDK) – All Four Heavy Flags Together"
priority: medium
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, get-merge-request, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3015: GitLab get_merge_request (SDK) – All Four Heavy Flags Together

**Module:** Gitlab · **Priority:** Medium · **Type:** Functional

**Objective:** Verify setting `include_discussions`, `include_approvals`, `include_pipelines`, and `include_commits` all `True` in a single call adds all four fields correctly, with no interference between them.

---

## Preconditions

- Same MR used in [[ELITEA-3014]], to allow direct comparison of per-field values.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `get_merge_request` (SDK) |
| Arguments | `include_discussions=True, include_approvals=True, include_pipelines=True, include_commits=True` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with all four flags `True` | Response contains `discussions`, `approvals`, `pipeline`, and `commits`, and nothing extra |
| 2 | Compare each field's value against the corresponding single-flag call in [[ELITEA-3014]] | Values are identical — no flag's presence alters another's output |

---

## Expected Final State

All four heavy fields can be requested together without interference.

---

## Pass/Fail Criteria

**Pass:** All four fields present and correct, matching their single-flag equivalents, nothing extra added.
**Fail:** Any field is missing, incorrect, or an unrelated field appears when all flags are combined.
