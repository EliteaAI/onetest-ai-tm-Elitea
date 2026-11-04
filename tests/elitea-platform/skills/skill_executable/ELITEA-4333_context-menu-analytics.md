---
id: ELITEA-4333
title: "Verify context menu 'Analytics' action navigates to run analytics page"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6927]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least one skill run exists in history
- Analytics page is implemented for skill runs

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all/[skillId]/history` |
| Analytics URL | `{{base_url}}/app/skills/all/[skillId]/history/analytics` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skill Run History page | Run History table displays |
| 2 | Click the three-dot menu icon on any run entry | Context menu opens |
| 3 | Verify "Analytics" option is visible | "Analytics" option appears |
| 4 | Click "Analytics" | System navigates to the analytics page for the selected run |
| 5 | Verify the URL changes to the analytics route | URL includes `/history/analytics` |
| 6 | Check that analytics data loads for the correct run | Analytics page displays metrics for the selected run |
| 7 | Verify analytics shows run-specific data (tokens, cost, model, duration) | Data is accurate and matches the run |

## Expected Final State

User is navigated to the analytics page showing detailed metrics for the selected skill run.

## Pass/Fail Criteria

**Pass:**
- "Analytics" option is available in context menu
- Clicking navigates to the analytics page
- Analytics page loads correctly
- Data displayed matches the selected run

**Fail:**
- "Analytics" option is missing or disabled
- Navigation does not occur or goes to wrong page
- Analytics page fails to load
- Data is incorrect or missing
