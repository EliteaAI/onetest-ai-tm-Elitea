---
id: ELITEA-4342
title: "Verify sorting by Runs column triggers backend API call to refetch data"
priority: critical
type: functional
module: analytics-skills
status: ready
execution_type: manual
tags: [feat:skills, feat:analytics, r-2.0.8, bug:7267]
requirements: [EliteaAI/elitea_issues#6929, EliteaAI/elitea_issues#7267]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least 20 skills exist with varying Runs and Spend values
- Default sort is by Spend (Top Spend skills)

## Test Data

| Field | Value |
|-------|-------|
| Analytics URL | `{{base_url}}/settings/analytics?tab=skills` |
| Skills Count | 20+ skills |
| Sort Columns | Runs, Spend |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Analytics → Skills tab | Skills analytics page loads |
| 2 | Open browser Developer Tools → Network tab | Network tab open, monitoring API requests |
| 3 | Observe initial page load: check API request to analytics_skills endpoint | API request sent: `GET /usage/analytics_skills/prompt_lib/{project_id}` with default sort (e.g., sort_by=spend) |
| 4 | Note the initial list of skills displayed (top 10 by Spend) | Skills listed in order of highest Spend first |
| 5 | Record the top 3 skill names displayed | Top 3 skills by Spend recorded |
| 6 | Click "RUNS" column header to sort by Runs | Sort indicator (arrow ↓) appears on "Runs" column |
| 7 | Check Network tab: verify a NEW API request is sent to analytics_skills endpoint | NEW API request sent: `GET /usage/analytics_skills/prompt_lib/{project_id}?sort_by=runs&sort_order=desc` |
| 8 | Verify query parameters include `sort_by=runs` and `sort_order=desc` | Parameters confirmed in request URL |
| 9 | Observe the updated list of skills displayed (top 10 by Runs) | Skills re-ordered: highest Runs values appear at top |
| 10 | Verify the top 3 skills by Runs are different from top 3 by Spend (if data allows) | Different skills appear (e.g., skill with high Runs but low Spend now visible) |
| 11 | Click "RUNS" column header again to toggle ascending sort | Sort indicator changes to arrow ↑ |
| 12 | Check Network tab: verify another NEW API request is sent with `sort_order=asc` | NEW API request sent with `sort_order=asc` |
| 13 | Verify skills with lowest Runs (including 0) appear at top | Skills re-ordered: lowest Runs first |

## Expected Final State

- Sorting by "Runs" triggers a new backend API call (not client-side re-sort)
- API request includes correct `sort_by` and `sort_order` parameters
- Skills list updates to reflect server-side sorted data
- Skills with high Runs but low Spend become visible after sorting by Runs

## Pass/Fail Criteria

**Pass:**
- Clicking "Runs" column triggers NEW backend API request
- API request includes `sort_by=runs` and `sort_order=desc` (or asc)
- Skills list updates based on server-side sorted data
- Different skills appear when sorting by Runs vs Spend (if data allows)
- Bug #7267 resolved: data refetched, not just client-side re-sort

**Fail:**
- No new API request sent when clicking "Runs" column (client-side sort only)
- API request missing `sort_by` or `sort_order` parameters
- Skills list does not change or only re-sorts existing loaded data
- Bug #7267 persists: high-run/low-spend skills remain hidden
