---
id: ELITEA-3612
title: "Tab Navigation - All Tabs Load Correctly"
priority: critical
type: functional
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, eng:frontend, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3612: Tab Navigation - All Tabs Load Correctly

**Module:** Per-Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify all tabs load correctly when clicked and switching between tabs works without errors.

## Preconditions

- Logged into {{base_url}}
- Per-Run Analytics page open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Per-Run Analytics. | Page loads with Costs tab active. |
| 2 | Click on "Tokens" tab. | Tokens tab becomes active, content loads. |
| 3 | Click on "Tools" tab. | Tools tab becomes active, content loads. |
| 4 | Click on "Health" tab. | Health tab becomes active, content loads. |
| 5 | Click on "Costs" tab. | Costs tab becomes active again. |
| 6 | Rapidly switch between tabs 5+ times. | Each tab loads correctly without errors. |
| 7 | Check browser console for errors. | No JavaScript errors logged. |
| 8 | Verify data values remain consistent. | Values don't change between switches. |

## Pass/Fail Criteria

**Pass:** All tabs load correctly on repeated switches, no errors, consistent data.
**Fail:** Errors appear, data changes unexpectedly, or tabs fail to load.
