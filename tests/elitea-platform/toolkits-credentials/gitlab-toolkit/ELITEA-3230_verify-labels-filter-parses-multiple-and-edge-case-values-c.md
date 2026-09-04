---
id: ELITEA-3230
title: "Verify labels filter parses multiple and edge-case values correctly"
priority: medium
type: functional
module: gitlab-toolkit
status: draft
execution_type: manual
tags: [r-2.0.6, int:gitlab]
requirements: [EliteaAI/elitea_issues#6213]
---

## Preconditions

- GitLab toolkit configured

## Test Data

| Field | Value |
|-------|-------|
| `labels` (space after comma) | `"bug, feature"` |
| `labels` (empty string) | `""` |
| `labels` (nonexistent label) | A label not present in the repo |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Invoke `get_issues` with `labels="bug, feature"` (containing a space after the comma) | The value is not treated as a single malformed label — issues matching either `bug` or `feature` are returned |
| 2 | Invoke `get_issues` with `labels=""` (empty string) | Behaves the same as omitting the parameter — no label filter applied, not an error |
| 3 | Invoke `get_issues` with a label that doesn't exist in the repo | An empty (not error) result is returned |

## Expected Final State

The comma-separated `labels` string is parsed and forwarded correctly for spaced, empty, and nonexistent-label edge cases.

## Pass/Fail Criteria

**Pass:**
- A space after the comma in `labels` does not break label matching
- An empty `labels` string behaves like an omitted parameter
- A nonexistent label returns an empty result, not an error

**Fail:**
- A space after the comma causes the label filter to match nothing or throw an error
- An empty `labels` string is treated as an active (and failing) filter
- A nonexistent label raises an error instead of returning empty
