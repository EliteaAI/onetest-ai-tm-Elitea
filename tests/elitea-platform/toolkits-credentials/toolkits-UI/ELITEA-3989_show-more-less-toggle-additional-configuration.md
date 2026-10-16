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
- "Show more" click reveals additional toolkit-specific fields
- Additional fields include embedding model, API version, etc.
- "Show less" collapses the additional fields
- Primary fields remain visible after collapse

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
| 2 | Verify only primary fields visible initially. | Toolkit Name, Description, Credentials visible. |
| 3 | Click "Show more" link. | Additional configuration fields appear. |
| 4 | Observe the additional fields revealed. | Fields like Embedding Model, API Version, Space, Limit, Labels, advanced settings visible. |
| 5 | Verify "Show more" changes to "Show less". | Link text changes to "Show less". |
| 6 | Click "Show less" link. | Additional fields collapse/hide. |
| 7 | Verify primary fields remain visible. | Toolkit Name, Description, Credentials still visible. |
| 8 | Verify "Show less" changes back to "Show more". | Link text changes back to "Show more". |

## Expected Final State

Configuration section returns to initial state with only primary fields visible and "Show more" link available.

## Pass/Fail Criteria

**Pass:**
- "Show more" reveals additional configuration fields
- Additional fields include toolkit-specific parameters
- "Show less" hides additional fields
- Primary fields always remain visible
- Link text toggles appropriately

**Fail:**
- "Show more" doesn't reveal additional fields
- "Show less" doesn't hide fields
- Primary fields disappear on toggle
- Link text doesn't change
