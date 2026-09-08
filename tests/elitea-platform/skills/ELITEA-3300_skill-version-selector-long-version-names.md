---
id: ELITEA-3300
title: "Skills version selector handles long version names gracefully"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:skills, feat:version-selector, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor or Admin role
- Skill with a version having a very long name exists (50+ characters)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Long version name | "production-release-candidate-with-bug-fixes-and-performance-improvements-v2.5.3" (70+ chars) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Skill with a version having a very long name | Skill loads |
| 2 | Open the version selector dropdown | Dropdown opens |
| 3 | Locate the version with the long name in the list | Long-named version visible |
| 4 | Verify the long name is displayed without breaking layout | Name displayed without UI breakage |
| 5 | Verify text either wraps to multiple lines or truncates with ellipsis | Text handling is appropriate (wrap or truncate) |
| 6 | If truncated, verify ellipsis (...) is visible at truncation point | Ellipsis indicates truncation |
| 7 | Hover over the truncated name | Hover action triggers |
| 8 | Verify a tooltip displays the full version name | Tooltip shows complete name |
| 9 | Verify metadata (timestamp, creator) remains visible and properly aligned | Metadata not obscured or misaligned |
| 10 | Verify icons (checkmark, pin) remain properly positioned | Icons in correct positions |
| 11 | Verify dropdown width doesn't expand excessively | Dropdown maintains reasonable width |

## Expected Final State

Long version names are displayed gracefully with either text wrapping or truncation with ellipsis. Tooltips reveal full names. Layout remains intact with metadata and icons properly positioned.

## Pass/Fail Criteria

**Pass:**
- Long names don't break layout
- Text wraps or truncates appropriately
- Ellipsis indicates truncation (if applicable)
- Tooltip shows full name on hover (if truncated)
- Metadata remains visible and aligned
- Icons positioned correctly
- Dropdown width controlled

**Fail:**
- Long names break layout or overflow
- No truncation or wrapping applied
- Missing ellipsis on truncated text
- No tooltip or incorrect tooltip
- Metadata obscured or misaligned
- Icon positioning broken
- Dropdown width expands excessively
