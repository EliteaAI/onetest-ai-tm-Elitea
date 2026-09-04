---
id: ELITEA-3218
title: "Verify page and per_page parameters paginate get_issues beyond the default cap"
priority: critical
type: functional
module: gitlab-toolkit
status: draft
execution_type: manual
tags: [r-2.0.6, int:gitlab]
requirements: [EliteaAI/elitea_issues#6213]
---

## Preconditions

- GitLab toolkit configured; test repository has 30+ issues
- GitLab Org toolkit configured for the parity check

## Test Data

| Field | Value |
|-------|-------|
| Scenario A | `per_page=100`, `page=1` |
| Scenario B | `per_page=10`, `page=1` then `page=2` |
| Scenario C | `page=999` (beyond last page) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In a repo with 30+ issues, invoke `get_issues` with `per_page=100`, `page=1` | All issues (up to 100) are returned in a single call, not capped at 20 |
| 2 | Invoke `get_issues` with `per_page=10`, `page=1` | First page of 10 issues returned |
| 3 | Invoke `get_issues` with `per_page=10`, `page=2` | Second page returns a distinct, non-overlapping set of 10 issues from page 1, together covering the expected total |
| 4 | Invoke `get_issues` with `page=999` (beyond the last page) | An empty result is returned, not an error |
| 5 | Repeat step 1 against the GitLab Org toolkit variant | Same behavior — up to 100 issues returned in a single call |

## Expected Final State

Explicit `page`/`per_page` values retrieve issue sets larger than the previous ~20-item cap, with correct, non-overlapping pagination and graceful handling of out-of-range pages.

## Pass/Fail Criteria

**Pass:**
- `per_page=100` returns up to 100 issues in one call
- Page 1 and page 2 with `per_page=10` return disjoint sets that together match the expected total
- A page beyond the last page returns an empty list, no error
- GitLab Org toolkit matches this behavior

**Fail:**
- Results remain capped at ~20 despite explicit `per_page`
- Pages 1 and 2 overlap or omit issues
- An out-of-range page raises an error instead of returning empty
