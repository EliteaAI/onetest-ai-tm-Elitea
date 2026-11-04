---
id: ELITEA-3989
title: "Show More/Less Toggle Reveals Additional Configuration"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-sections-redesign, configuration, toggle]
requirements: [EL-6252]
---
# ELITEA-3989: Show More/Less Toggle Reveals Additional Configuration

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that "Show more" expands additional configuration fields and "Show less" collapses them back.

**Coverage:**
- "Show less" collapses the additional fields
- "Show more" expands the additional fields again
- Primary fields remain visible throughout

## Preconditions

- Logged in to {{base_url}}
- A toolkit with multiple configuration parameters exists

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with additional configuration fields |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → open any toolkit. | Toolkit details page opens with Configuration expanded. |
| 2 | Verify all fields visible initially, with "Show less" link present. | Toolkit Name, Description, Credentials, and additional fields (e.g., Embedding Model, API Version, Space, Limit, Labels, advanced settings) all visible. |
| 3 | Click "Show less" link. | Additional fields collapse/hide. |
| 4 | Verify "Show less" changes to "Show more". | Link text changes to "Show more". |
| 5 | Verify primary fields remain visible. | Toolkit Name, Description, Credentials still visible. |
| 6 | Click "Show more" link. | Additional fields expand again. |
| 7 | Verify "Show more" changes back to "Show less". | Link text changes back to "Show less". |

## Expected Final State

Configuration section returns to initial state with all fields visible and "Show less" link available.

## Pass/Fail Criteria

**Pass:**
- "Show less" hides additional configuration fields
- "Show more" reveals them again, including toolkit-specific parameters
- Primary fields always remain visible
- Link text toggles appropriately

**Fail:**
- "Show less" doesn't hide additional fields
- "Show more" doesn't reveal fields again
- Primary fields disappear on toggle
- Link text doesn't change
