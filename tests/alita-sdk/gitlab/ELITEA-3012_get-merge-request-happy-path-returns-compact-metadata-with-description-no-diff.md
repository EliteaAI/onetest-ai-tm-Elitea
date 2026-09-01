---
id: ELITEA-3012
title: "GitLab get_merge_request (SDK) – Happy Path Returns Compact Metadata Incl. description, No Diff"
priority: high
type: functional
module: gitlab
status: draft
execution_type: manual
tags: [sdk, gitlab, merge-requests, get-merge-request, issue:6212]
requirements: [EliteaAI/elitea_issues#6212]
---

# ELITEA-3012: GitLab get_merge_request (SDK) – Happy Path Returns Compact Metadata Incl. description, No Diff

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify `get_merge_request` returns full compact metadata (including `description`) for a valid MR IID, across an open MR, a closed-not-merged MR, and an older MR, with no diff content.

---

## Preconditions

- GitLab toolkit configured against a repository with at least one open MR, one closed (not merged) MR, and one older MR.

---

## Test Data

| Field | Value |
|-------|-------|
| Method | `get_merge_request` (SDK) |
| Calls | `pr_number=<open MR IID>`, `pr_number=<recent closed/other MR IID>`, `pr_number=<oldest MR IID, e.g. 1>` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with a valid open MR's IID | Returns metadata including `description`, no diff content |
| 2 | Call with a second valid MR's IID | Returns metadata correctly for that MR |
| 3 | Call with the oldest MR's IID (e.g. `1`, closed) | Returns metadata correctly even for the oldest/closed MR |

---

## Expected Final State

`get_merge_request` returns correct, complete compact metadata for any valid MR IID regardless of age/state.

---

## Pass/Fail Criteria

**Pass:** All three calls return correct metadata incl. `description`, no diff content.
**Fail:** Any call errors, returns metadata for the wrong MR, omits `description`, or includes diff content.
