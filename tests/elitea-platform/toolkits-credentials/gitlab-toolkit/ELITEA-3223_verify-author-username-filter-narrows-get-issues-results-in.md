---
id: ELITEA-3223
title: "Verify author_username filter narrows get_issues results including case-sensitivity and unknown-author handling"
priority: high
type: functional
module: gitlab-toolkit
status: draft
execution_type: manual
tags: [r-2.0.6, int:gitlab]
requirements: [EliteaAI/elitea_issues#6213]
---

## Preconditions

- GitLab toolkit and GitLab Org toolkit configured
- Test repository has issues authored by at least 2 distinct users (add a second-author issue if the dataset is single-author, so real narrowing can be exercised)

## Test Data

| Field | Value |
|-------|-------|
| `author_username` (known, exact case) | `<known test author>` |
| `author_username` (mixed case) | `MixedCase` vs `mixedcase` |
| `author_username` (nonexistent) | `<never-authored-username>` |
| Combined filters | `state=closed`, `labels=bug`, `author_username=<user>` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Invoke `get_issues` with `author_username=<known test author>` (exact case as stored in GitLab) | Only issues created by that user are returned |
| 2 | Invoke `get_issues` with the same username but different letter casing (e.g. `MixedCase` vs `mixedcase`) | The match behavior (case-sensitive or case-insensitive) is observed and confirmed to match documented/intended behavior rather than being an unverified assumption |
| 3 | Invoke `get_issues` with `author_username` set to a username that has never authored any issue in the repo | An empty result is returned, not an error |
| 4 | Combine `author_username` with `labels` and `state` in a single call (e.g. `state=closed` + `labels=bug` + `author_username=<user>`) | Results satisfy all filters simultaneously (AND semantics) |
| 5 | Repeat steps 1–4 against the GitLab Org toolkit | Same filtering behavior is observed |

## Expected Final State

`author_username` correctly narrows results, its casing behavior is confirmed and documented, unknown authors yield an empty (not error) result, and it combines correctly with other filters, on both toolkits.

## Pass/Fail Criteria

**Pass:**
- Filtering by a known author returns only that author's issues
- Case-sensitivity behavior is consistent and matches intended/documented behavior
- An unknown author returns an empty result, no error
- Combined filters apply together correctly
- GitLab Org toolkit matches this behavior

**Fail:**
- Issues from other authors leak into a filtered result
- Case handling is inconsistent or undocumented/unexpected
- An unknown author causes an error instead of an empty result
- Combined filters are not all applied
