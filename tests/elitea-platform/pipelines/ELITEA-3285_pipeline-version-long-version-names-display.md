---
id: ELITEA-3285
title: "Pipeline version dropdown handles long version names without breaking layout"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:pipelines, feat:version-selector, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor/Admin role
- Private project context is selected
- Pipeline exists with a version having a very long name (50+ characters)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Pipeline | Pipeline with versions including long names |
| Long version name | "production-deployment-2026-Q1-hotfix-version-final-approved-release-candidate-3" (70+ chars) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create or navigate to a Pipeline with a version having a very long name | Pipeline loads |
| 2 | Open the version selector dropdown | Dropdown opens |
| 3 | Locate the version with the long name in the list | Long version name is visible |
| 4 | Verify the long name is displayed without breaking the dropdown layout | Layout remains intact |
| 5 | Verify text wraps to multiple lines OR truncates with ellipsis | Text handling is graceful (wrap or ellipsis) |
| 6 | If truncated, hover over the truncated name | Tooltip appears showing full name (if applicable) |
| 7 | Verify metadata (timestamp, creator) remains visible and properly aligned | Metadata is not obscured or misaligned |
| 8 | Verify icons (checkmark, pin) remain properly positioned | Icons are in correct positions |
| 9 | Verify dropdown width doesn't expand excessively | Dropdown width is controlled and reasonable |
| 10 | Select the version with the long name | Version is selected successfully |
| 11 | Verify the selector button/field handles the long name appropriately | Selector displays name with truncation or wrapping |

## Expected Final State

Long version names are handled gracefully with text wrapping or truncation (with ellipsis and optional tooltip). Layout remains intact and usable.

## Pass/Fail Criteria

**Pass:**
- Long version names don't break dropdown layout
- Text wraps or truncates appropriately (ellipsis if truncated)
- Tooltip shows full name on hover (if truncated)
- Metadata and icons remain properly positioned
- Dropdown width is controlled
- Version selection works correctly
- Selector button handles long names gracefully

**Fail:**
- Long names break dropdown layout
- Text overflows outside boundaries
- Dropdown expands excessively
- Metadata or icons are misaligned or hidden
- No truncation or wrapping is applied
- Tooltip doesn't show full name when needed
- Version selection fails
