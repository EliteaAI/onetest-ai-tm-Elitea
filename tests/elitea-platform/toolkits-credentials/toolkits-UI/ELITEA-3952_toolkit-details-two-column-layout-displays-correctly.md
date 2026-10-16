---
id: ELITEA-3952
title: "Toolkit Details Two-Column Layout Displays Correctly"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, smoke, layout]
requirements: []
---
# ELITEA-3952: Toolkit Details Two-Column Layout Displays Correctly

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional / Smoke

**Objective:** Verify that the redesigned Toolkit Details page displays the correct two-column layout with configuration/tools on the left side and indexes panel on the right side.

**Coverage:**
- Two-column layout structure renders correctly
- Left panel contains toolkit configuration and tools section
- Right panel contains indexes section
- Configuration section header is NOT displayed (removed per design)
- Layout is responsive and panels are properly separated

## Preconditions

- Logged in to {{base_url}} with a valid user account
- At least one toolkit exists in the project
- User has permission to view/edit toolkits

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any existing toolkit (e.g., GitHub, Jira, ADO, Confluence) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to {{base_url}}/app/ → Toolkits & Indexes from the left sidebar. | Toolkits & Indexes list page displays. |
| 2 | Click on any existing toolkit to open its details page. | Toolkit details page opens with two-column layout. |
| 3 | Observe the left side of the page. | Left panel displays: Toolkit Name field, Description field, Credentials dropdown, "Show more" link, Form/Raw JSON toggle, and TOOLS section with count (e.g., "20/22"). |
| 4 | Observe the right side of the page. | Right panel displays: "Indexes" header with count format "Indexes (N)" where N is number of indexes. |
| 5 | Verify the "Configuration" section header is NOT present above the form fields. | No "Configuration" header is displayed; form fields start directly with Toolkit Name. |
| 6 | Verify the columns are visually separated and have proper spacing. | Clear visual separation between left (config/tools) and right (indexes) columns. |

## Expected Final State

Toolkit details page displays a clean two-column layout with configuration and tools on the left, indexes on the right, and no "Configuration" section header.

## Pass/Fail Criteria

**Pass:**
- Two-column layout is properly rendered
- Left column contains all configuration fields and TOOLS section
- Right column contains Indexes panel
- No "Configuration" header is visible
- Layout has proper spacing and visual separation

**Fail:**
- Single-column or incorrect layout structure
- "Configuration" header is still visible
- Panels overlap or have no visual separation
- Missing sections in either column
