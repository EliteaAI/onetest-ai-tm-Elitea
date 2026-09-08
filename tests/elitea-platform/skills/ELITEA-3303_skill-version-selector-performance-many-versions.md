---
id: ELITEA-3303
title: "Skills version selector performs well with 50+ versions"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:skills, feat:version-selector, feat:performance, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor or Admin role
- Skill with 50+ versions exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Test Skill | Skill with 50 or more versions |
| Performance thresholds | Dropdown open: < 2 seconds, Search: < 1 second |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Skill with 50+ versions | Skill loads |
| 2 | Note the current time | Timestamp noted |
| 3 | Click to open the version selector dropdown | Dropdown begins to open |
| 4 | Measure time until dropdown is fully rendered | Dropdown opens in < 2 seconds |
| 5 | Verify all 50+ versions are displayed | Complete version list visible |
| 6 | Scroll through the version list | Scrolling action initiated |
| 7 | Verify scrolling is smooth and responsive | No lag or stuttering during scroll |
| 8 | Scroll to bottom of list | Bottom reached smoothly |
| 9 | Scroll back to top | Top reached smoothly |
| 10 | Type a search query in the search field | Search input entered |
| 11 | Measure time until filtered results appear | Results appear in < 1 second |
| 12 | Verify search filtering is fast and responsive | No noticeable delay in filtering |
| 13 | Clear search and verify list restores quickly | Full list restores quickly |
| 14 | Select a version from the list | Version selection initiated |
| 15 | Verify version selection works correctly and quickly | Selection completes without delay |
| 16 | Check browser console for performance warnings | No performance warnings or errors |

## Expected Final State

Version selector dropdown remains responsive and usable with 50+ versions. Opening, scrolling, searching, and selecting all perform within acceptable time thresholds with no lag or UI freezing.

## Pass/Fail Criteria

**Pass:**
- Dropdown opens in < 2 seconds
- All 50+ versions load and display
- Scrolling is smooth with no lag
- Search filtering completes in < 1 second
- Version selection works quickly
- No performance warnings in console
- UI remains responsive throughout

**Fail:**
- Dropdown takes > 2 seconds to open
- UI freezes or becomes unresponsive
- Scrolling is laggy or stutters
- Search takes > 1 second to filter
- Version selection is slow
- Performance warnings or errors in console
- Browser becomes sluggish
