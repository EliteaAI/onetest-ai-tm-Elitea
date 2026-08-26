---
id: ELITEA-2812
title: "Configuration Section Expanded by Default with Primary Fields"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-sections-redesign, configuration, layout]
requirements: [EL-6252]
---
# ELITEA-2812: Configuration Section Expanded by Default with Primary Fields

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Configuration section is expanded by default when opening a Toolkit, showing only primary fields with "Show more" link available.

**Coverage:**
- Configuration section expanded on page load
- Only primary fields visible initially (Toolkit Name, Description, Credentials)
- Credentials displayed as dropdown (PGVector)
- "Show more" link visible for additional fields

## Preconditions

- Logged in to {{base_url}}
- At least one toolkit exists in the project

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any existing toolkit (e.g., GitHub, Jira, ADO) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes from the left sidebar. | Toolkits list page displays. |
| 2 | Click on any existing toolkit to open its details page. | Toolkit details page opens. |
| 3 | Observe the Configuration section state on page load. | Configuration section is expanded by default. |
| 4 | Verify primary fields visible: Toolkit Name, Description, Credentials. | All three primary fields are displayed. |
| 5 | Verify Credentials field is displayed as a dropdown. | Credentials shows as dropdown selector (e.g., PGVector). |
| 6 | Verify "Show more" link is visible below primary fields. | "Show more" link/button is present. |
| 7 | Verify no additional configuration fields are visible initially. | Only primary fields shown; advanced settings hidden. |

## Expected Final State

Configuration section is expanded by default showing only Toolkit Name, Description, and Credentials (as dropdown), with "Show more" link available for additional fields.

## Pass/Fail Criteria

**Pass:**
- Configuration section expanded on page load
- Only 3 primary fields visible initially
- Credentials displayed as dropdown
- "Show more" link visible

**Fail:**
- Configuration section collapsed on load
- Additional fields visible by default
- Credentials not displayed as dropdown
- "Show more" link missing
