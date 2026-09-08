---
id: ELITEA-3288
title: "Pipeline version dropdown performs well with 50+ versions"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:pipelines, feat:version-selector, feat:performance, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor/Admin role
- Private project context is selected
- Pipeline exists with 50+ versions (create test data if necessary)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Pipeline | Pipeline with 50+ versions |
| Performance threshold (dropdown open) | < 2 seconds |
| Performance threshold (search filter) | < 1 second |

## Steps: Dropdown Opening Performance

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Pipeline with 50+ versions | Pipeline loads |
| 2 | Click the version selector to open the dropdown | Dropdown begins opening |
| 3 | Measure time until dropdown is fully rendered | Dropdown opens in < 2 seconds |
| 4 | Verify all 50+ versions are visible in the list | All versions are rendered |
| 5 | Check browser console for performance warnings or errors | No errors or warnings |

## Steps: Scrolling Performance

| # | Action | Expected Result |
|---|--------|-----------------|
| 6 | Scroll down through the version list | Scrolling is smooth and responsive |
| 7 | Scroll quickly from top to bottom | No lag or stuttering |
| 8 | Scroll back up from bottom to top | Scrolling remains smooth |
| 9 | Verify all version entries render correctly during scroll | No missing or broken entries |

## Steps: Search Performance

| # | Action | Expected Result |
|---|--------|-----------------|
| 10 | Type a search query that matches many versions (e.g., "v") | Search begins filtering |
| 11 | Measure time until filtered results are displayed | Results appear in < 1 second |
| 12 | Type a different search query | Filtering updates quickly |
| 13 | Clear the search field | Full list returns quickly (< 1 second) |

## Steps: Selection Performance

| # | Action | Expected Result |
|---|--------|-----------------|
| 14 | Select a version from the dropdown (near the end of the list) | Version is selected |
| 15 | Verify the Pipeline canvas updates without significant delay | Canvas updates smoothly |
| 16 | Open the dropdown again | Dropdown opens quickly |
| 17 | Select a different version | Selection is processed quickly |

## Expected Final State

Version selector dropdown remains responsive and usable with 50+ versions. Opening, scrolling, searching, and selecting all perform within acceptable thresholds.

## Pass/Fail Criteria

**Pass:**
- Dropdown opens in < 2 seconds with 50+ versions
- Scrolling is smooth and responsive
- Search filtering completes in < 1 second
- Version selection works correctly
- No performance warnings or errors in console
- User experience is smooth and responsive

**Fail:**
- Dropdown takes > 2 seconds to open
- Scrolling is laggy or stutters
- Search takes > 1 second to filter
- Version selection is slow or fails
- Performance warnings or errors in console
- User experience is degraded with many versions
