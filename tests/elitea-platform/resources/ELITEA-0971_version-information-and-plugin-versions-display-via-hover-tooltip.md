---
id: ELITEA-0971
title: "Version Information and Plugin Versions Display via Hover Tooltip"
priority: critical
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0971: Version Information and Plugin Versions Display via Hover Tooltip

**Module:** Resources · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that hovering over the (i) icon in the page header reveals a tooltip listing all 6 component versions (elitea_core, admin, notifications, configurations, sdk_plugin, indexer_worker), and that the tooltip dismisses on mouse-out.

**Coverage:**
- (i) icon visibility in page header
- Hover-triggered tooltip display
- 6 component names and non-empty version values
- Tooltip auto-dismiss on cursor move-away

## Preconditions

Logged in to ELITEA; on the Resources page

## Test Data

Expected tooltip components: elitea_core, admin, notifications, configurations, sdk_plugin, indexer_worker
Version string format: Version: X.X.X (DD-Mon-YYYY)
Tooltip trigger: hover only (not click)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Resources page. | Resources page loads. |
| 2 | Locate the page header area containing the version string (format: Version: X.X.X (DD-Mon-YYYY)). | Version string is visible in the header. |
| 3 | Locate the small circular (i) information icon next to the version string. | (i) icon is visible. |
| 4 | Move the mouse cursor over the (i) icon (hover; do NOT click). | A tooltip or popover appears without requiring a click. |
| 5 | Read the tooltip content and confirm all 6 component names are listed: elitea_core, admin, notifications, configurations, sdk_plugin, indexer_worker. | All 6 component names are present in the tooltip. |
| 6 | Confirm each component entry has a non-empty version value (e.g., a version number string). | Every component shows a non-blank version value. |
| 7 | Move the mouse cursor away from the (i) icon to an empty area of the page. | The tooltip disappears (auto-dismisses on mouse-out). |
| 8 | Confirm the page remains stable (no crash, no spinner, no error). | Page is fully functional after tooltip interaction. |

## Expected Final State

Page is fully functional after tooltip interaction.

## Pass/Fail Criteria

**Pass:**
- (i) icon is visible in the page header
- Hovering (i) icon shows tooltip with all 6 components and non-empty version values
- Tooltip disappears when cursor moves away from icon
- Page remains stable throughout

**Fail:**
- (i) icon is absent
- Tooltip does not appear on hover
- Any component name is missing from the tooltip
- Any version value is blank or null
- Tooltip requires a click to trigger
- Tooltip does not dismiss on mouse-out
