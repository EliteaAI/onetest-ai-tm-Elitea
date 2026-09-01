---
id: ELITEA-3016
title: "GitLab get_merge_request (SDK) – Heavy-Field Failure Falls Back to an Error String, Not the Normal Dict/List Shape"
priority: high
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, get-merge-request, issue:6212, new]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3016: GitLab get_merge_request (SDK) – Heavy-Field Failure Falls Back to an Error String, Not the Normal Dict/List Shape

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a heavy-field fetch (`include_discussions`/`include_approvals`/`include_pipelines`/`include_commits`) fails internally, the corresponding key's value becomes a **string** (`"Unable to retrieve <field>: {e}"`) instead of its normal shape (list/dict) — and confirm this type inconsistency is the actual, intended contract rather than an unhandled bug, since a caller expecting a consistent type could break on it.

---

## Preconditions

- A way to force one heavy-field sub-fetch to fail without failing the whole `get_merge_request` call — e.g. an MR/pipeline combination with restricted permissions on discussions/approvals/pipelines/commits, or a project where one of those sub-resources is disabled.
- If no such repository/permission combination is available in this environment, mark this test **inconclusive** rather than skip it silently — this is one of the more consequential untested edge cases in the implementation.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `get_merge_request` (SDK) |
| Arguments | the heavy flag whose underlying sub-fetch can be forced to fail, `=True` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Trigger a call where one heavy-field sub-fetch fails | Call does not raise; the overall `get_merge_request` result still returns |
| 2 | Inspect the type of the failed field's value | Value is a plain string starting with `"Unable to retrieve"`, not a list/dict |
| 3 | Confirm all other requested heavy fields (that did not fail) still have their normal shape | Only the failed field's shape changes; others are unaffected |

---

## Expected Final State

A single heavy-field failure degrades that one field to an error string without failing the whole call or affecting sibling fields — documented and confirmed as the intended contract.

---

## Pass/Fail Criteria

**Pass:** Failed field becomes an error string as documented in the code; other fields keep their normal shape; whole call does not raise.
**Fail:** The type inconsistency causes a downstream consumer-facing crash in normal usage, or the failure instead propagates as an unhandled exception for the whole call.
