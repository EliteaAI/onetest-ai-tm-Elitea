---
id: ELITEA-2814
title: "Configuration Field Values Preserved on Show More/Less Toggle"
priority: high
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-sections-redesign, configuration, data-preservation]
requirements: [EL-6252]
---
# ELITEA-2814: Configuration Field Values Preserved on Show More/Less Toggle

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify that unsaved field values are preserved when toggling Show more/less without saving.

**Coverage:**
- Modified values in additional fields preserved during toggle
- No data loss when collapsing/expanding
- Unsaved changes indicator remains active

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with multiple configuration parameters exists

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with editable additional fields |
| Test Value | Modified value for an additional field |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → open any toolkit. | Toolkit details page opens. |
| 2 | Click "Show more" to reveal additional fields. | Additional configuration fields appear. |
| 3 | Modify an additional field value (e.g., change API version or limit) without saving. | Field value changes; unsaved changes indicator may appear. |
| 4 | Note the modified value. | Value recorded for verification. |
| 5 | Click "Show less" to collapse additional fields. | Additional fields hide. |
| 6 | Click "Show more" again. | Additional fields reappear. |
| 7 | Verify the modified field retains its value. | Previously modified value is preserved, not reset to original. |
| 8 | Modify a primary field (e.g., Description) without saving. | Primary field value changes. |
| 9 | Toggle Show more/less multiple times. | All modified values preserved across toggles. |

## Expected Final State

All unsaved modifications to both primary and additional fields are preserved across Show more/less toggles.

## Pass/Fail Criteria

**Pass:**
- Modified additional field values preserved after toggle
- Modified primary field values preserved
- No data loss on multiple toggles
- Unsaved changes state maintained

**Fail:**
- Field values reset to original on toggle
- Data lost when collapsing/expanding
- Unsaved changes indicator disappears incorrectly
