---
id: ELITEA-3273
title: "Agent — Version Selector Performance with Large List"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:version-selector, nfr:performance, feat:agents, issue:6302]
requirements: [EliteaAI/elitea_issues#6302]
---
# ELITEA-3273: Agent — Version Selector Performance with Large List

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the version selector dropdown remains responsive and usable when an Agent has a large number of versions (50+ versions).

## Preconditions

- User logged in to ELITEA ({{base_url}})
- Agent exists with 50+ versions (create via automation or manual process if needed)
- User has permission to view and switch versions

## Test Data

| Field | Value |
|-------|-------|
| Test Agent | Agent with ≥50 versions |
| Version Count | 50+ versions |
| Performance Thresholds | Dropdown open: <2s; Search filtering: <1s |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent with 50+ versions | Agent page loads successfully |
| 2 | Click the version selector to open the dropdown | Dropdown opens without significant delay (<2 seconds) |
| 3 | Observe the rendering of the version list | All versions render correctly; no visual glitches |
| 4 | Scroll through the version list from top to bottom | Scrolling is smooth and responsive; no lag or stuttering |
| 5 | Scroll back to the top of the list | Scrolling remains smooth in reverse direction |
| 6 | Type a search query that matches multiple versions (e.g., "v") | Search filtering is fast (<1 second); filtered results display quickly |
| 7 | Type another search query (e.g., "production") | Search filtering remains fast |
| 8 | Clear the search | Full list reappears quickly |
| 9 | Select a version from the middle of the list | Version is selected without delay; dropdown closes; interface updates to selected version |
| 10 | Check browser console for performance warnings or errors | No console errors or performance warnings |

## Expected Final State

Dropdown opens quickly (<2s); scrolling is smooth; search filtering is fast (<1s); version selection works correctly; no performance issues.

## Pass/Fail Criteria

**Pass:** Dropdown opens in <2 seconds; scrolling is smooth; search filtering in <1 second; version selection works correctly; no console errors

**Fail:** Dropdown takes >2 seconds to open; scrolling is laggy; search filtering takes >1 second; version selection fails or is slow; console errors occur

**Note:** If creating 50+ versions manually is not feasible, document the maximum number of versions tested and performance observations.
