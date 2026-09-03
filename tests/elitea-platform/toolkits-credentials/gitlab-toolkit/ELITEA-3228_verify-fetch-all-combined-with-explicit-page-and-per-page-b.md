---
id: ELITEA-3228
title: "Verify fetch_all combined with explicit page and per_page behaves predictably"
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
- Test repository has a known total matching issue count

## Test Data

| Field | Value |
|-------|-------|
| `fetch_all` | `True` |
| `page` | `2` |
| `per_page` | `5` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Invoke `get_issues` with `fetch_all=True`, `page=2`, `per_page=5` on the plain GitLab toolkit | Call completes successfully |
| 2 | Verify the full matching issue set is returned | `page`/`per_page` had no effect — the complete set is returned, not just page 2's 5 items |
| 3 | Repeat the same call on the GitLab Org toolkit | Same full-set behavior is observed, consistent with the plain GitLab toolkit |

## Expected Final State

When a caller mistakenly supplies both `fetch_all=True` and explicit `page`/`per_page`, the tool ignores pagination as designed and returns the full matching set, consistently across both toolkits.

## Pass/Fail Criteria

**Pass:**
- The full matching issue set is returned despite explicit `page`/`per_page` values
- Behavior is consistent between the plain GitLab and GitLab Org toolkits

**Fail:**
- The result is limited to the specified page/per_page instead of the full set
- Behavior differs between the two toolkits
