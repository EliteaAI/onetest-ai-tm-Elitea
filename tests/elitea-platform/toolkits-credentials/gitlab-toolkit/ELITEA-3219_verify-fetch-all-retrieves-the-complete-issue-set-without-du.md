---
id: ELITEA-3219
title: "Verify fetch_all retrieves the complete issue set without duplicates or omissions"
priority: critical
type: functional
module: gitlab-toolkit
status: draft
execution_type: manual
tags: [r-2.0.6, int:gitlab]
requirements: [EliteaAI/elitea_issues#6213]
---

## Preconditions

- GitLab toolkit and GitLab Org toolkit configured
- A test repository with more than 100 issues, or the largest available test repository

## Test Data

| Field | Value |
|-------|-------|
| `fetch_all` | `True` |
| `state` | `all` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Invoke `get_issues` with `fetch_all=True` and `state=all` on the largest available test repo | Call completes successfully, auto-paginating across all pages |
| 2 | Cross-check the number of issues returned against the true total count of matching issues in GitLab (via GitLab UI or API) | Counts match exactly |
| 3 | Scan the returned issue numbers | No issue number appears more than once |
| 4 | Repeat with explicit `page`/`per_page` values also passed alongside `fetch_all=True` | The explicit `page`/`per_page` values are not honored — pagination is fully bypassed |
| 5 | Repeat steps 1–3 against the GitLab Org toolkit variant | Same complete, deduplicated result is returned |

## Expected Final State

`fetch_all=True` returns every matching issue exactly once across all pages, ignoring any explicit pagination parameters, on both toolkits.

## Pass/Fail Criteria

**Pass:**
- Returned issue count matches the true total in GitLab
- No issue number is duplicated
- Explicit `page`/`per_page` have no effect when `fetch_all=True` is set
- GitLab Org toolkit matches this behavior

**Fail:**
- Any issue is missing or duplicated
- The result is silently truncated below the true total
- Explicit `page`/`per_page` override or interfere with `fetch_all=True`
