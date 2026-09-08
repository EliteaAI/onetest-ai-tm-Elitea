---
id: ELITEA-3301
title: "Skills version selector handles long creator names and emails gracefully"
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
- Version exists with a creator having a very long name or email address

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Long creator name | "Christopher Alexander Montgomery-Williamson III" |
| Long email | "christopher.alexander.montgomery-williamson@example-company.com" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skill with version created by user with long name/email | Skill loads |
| 2 | Open the version selector dropdown | Dropdown opens |
| 3 | Locate version with long creator information | Version visible |
| 4 | Verify creator information is displayed without breaking layout | Creator info displayed cleanly |
| 5 | Verify text wraps or truncates appropriately | Text handling is appropriate |
| 6 | If truncated, verify ellipsis is visible | Ellipsis indicates truncation |
| 7 | Verify other metadata (version name, timestamp) remains visible and aligned | Other metadata not affected |
| 8 | Verify the version row height adjusts appropriately if text wraps | Row height accommodates wrapped text |
| 9 | Verify icons (checkmark, pin) remain properly positioned | Icons positioned correctly |

## Expected Final State

Long creator names and email addresses are displayed without breaking the layout. Text wraps or truncates appropriately while maintaining alignment of all metadata elements.

## Pass/Fail Criteria

**Pass:**
- Long creator info doesn't break layout
- Text wraps or truncates appropriately
- Ellipsis visible if truncated
- Version name and timestamp remain visible
- Row height adjusts if needed
- Icons positioned correctly
- Overall layout remains clean

**Fail:**
- Long creator info breaks layout
- Text overflows container
- Other metadata obscured
- Row height doesn't accommodate content
- Icons misaligned
- Layout appears broken
