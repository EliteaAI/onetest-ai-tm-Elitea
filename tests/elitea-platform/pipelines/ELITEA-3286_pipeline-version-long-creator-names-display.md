---
id: ELITEA-3286
title: "Pipeline version dropdown handles long creator names/emails without breaking layout"
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
- Pipeline exists with a version created by a user with a very long name or email address

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Pipeline | Pipeline with versions created by users with long names/emails |
| Long creator name | "Christopher Alexander Montgomery-Wellington III" |
| Long creator email | "christopher.alexander.montgomery-wellington@very-long-company-domain-name.com" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Pipeline with a version created by a user with a long name/email | Pipeline loads |
| 2 | Open the version selector dropdown | Dropdown opens |
| 3 | Locate the version with the long creator information | Version entry is visible |
| 4 | Verify the creator information is displayed without breaking the layout | Layout remains intact |
| 5 | Verify text wraps or truncates appropriately | Text handling is graceful (wrap or ellipsis) |
| 6 | Verify other metadata (version name, timestamp) remains visible and aligned | All metadata is visible and properly positioned |
| 7 | Verify the long creator text doesn't overlap with other elements | No overlap with icons or other text |
| 8 | Verify dropdown width is controlled and doesn't expand excessively | Dropdown width is reasonable |
| 9 | Search for the long creator name or email | Search finds the version correctly |
| 10 | Verify search results display the long creator information correctly | Creator info is displayed properly in search results |

## Expected Final State

Long creator names and email addresses are handled gracefully with text wrapping or truncation. Layout remains intact and all metadata is visible.

## Pass/Fail Criteria

**Pass:**
- Long creator names/emails don't break dropdown layout
- Text wraps or truncates appropriately
- Other metadata (version name, timestamp) remains visible
- No overlap with icons or other elements
- Dropdown width is controlled
- Search functionality works with long creator info
- Layout is clean and readable

**Fail:**
- Long creator info breaks dropdown layout
- Text overflows outside boundaries
- Other metadata is obscured or misaligned
- Text overlaps with icons or other elements
- Dropdown expands excessively
- Search doesn't handle long creator info correctly
- Layout is cluttered or unreadable
