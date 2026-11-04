---
id: ELITEA-4408
title: "Navigate from own skill Run History to Analytics page"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, navigation]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has created at least one skill
- Skill has execution history with at least one completed run

## Test Data

| Field | Value |
|-------|-------|
| Base URL | `{{base_url}}` |
| Expected Analytics URL | `/skills/:tab/:skillId/history/analytics` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills section from left sidebar | Skills page displays |
| 2 | Select any skill from "My Skills" list | Skill detail page opens |
| 3 | Click "Run History" tab | Run History table displays with list of runs |
| 4 | Locate any completed run entry in the history table | Run entry is visible |
| 5 | Click the three-dot menu (⋮) on the run row | Context menu opens with options |
| 6 | Click "Analytics" option from dropdown menu | System navigates to analytics page |
| 7 | Verify URL format matches `/skills/:tab/:skillId/history/analytics` | URL is correct |
| 8 | Verify analytics page displays data for the selected run | Page loads with run-specific metrics |
| 9 | Check browser console for errors | No console errors present |

## Expected Final State

Analytics page is displayed with:
- Correct URL format
- Run-specific data loaded
- No navigation errors
- No console errors

## Pass/Fail Criteria

**Pass:**
- Analytics menu option is available and clickable
- Navigation to analytics page succeeds
- URL format is `/skills/:tab/:skillId/history/analytics`
- Page displays analytics data for correct run
- No console errors

**Fail:**
- Analytics option missing or disabled
- Navigation fails or goes to wrong page
- URL format is incorrect
- Wrong run data displayed
- Console errors present
