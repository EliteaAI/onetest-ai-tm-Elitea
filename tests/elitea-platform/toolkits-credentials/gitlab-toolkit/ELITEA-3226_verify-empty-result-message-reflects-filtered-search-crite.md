---
id: ELITEA-3226
title: "Verify empty-result message reflects filtered search criteria"
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

## Test Data

| Field | Value |
|-------|-------|
| `labels` (guaranteed empty match) | `nonexistent-label-xyz` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Invoke `get_issues` with a filter combination guaranteed to match nothing (e.g. `labels=nonexistent-label-xyz`) on the plain GitLab toolkit | Response text reads "No issues found matching the given filters" rather than the old "No open issues available" |
| 2 | Repeat the same call against the GitLab Org toolkit | Response text reads "No issues found matching the given filters" rather than the old "No open issues available" |

## Expected Final State

Both toolkits return the updated, filter-aware empty-result message instead of the legacy "no open issues" message.

## Pass/Fail Criteria

**Pass:**
- Both toolkits return "No issues found matching the given filters" for a zero-match filtered query

**Fail:**
- Either toolkit still returns the old "No open issues available" message
- Any other unexpected message or an error is returned for a valid zero-match query
