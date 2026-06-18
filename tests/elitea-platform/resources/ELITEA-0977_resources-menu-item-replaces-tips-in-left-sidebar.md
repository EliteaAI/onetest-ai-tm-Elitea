---
id: ELITEA-0977
title: "Resources Menu Item Replaces Tips in Left Sidebar"
priority: critical
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0977: Resources Menu Item Replaces Tips in Left Sidebar

**Module:** Resources · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the old "Tips" menu item is removed and "Resources" appears immediately after "Settings" in the left sidebar.

**Coverage:**
- Tips menu removal
- Resources menu presence
- Sidebar order validation (Settings → Resources → Notifications)

## Preconditions

Logged in as a standard ELITEA user
Browser: Chrome or Firefox (latest stable)
Environment: next.elitea.ai or designated QA environment

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA with valid credentials. | Home page loads with the left sidebar visible. |
| 2 | Scan the full list of left sidebar navigation items from top to bottom. | All sidebar items are visible. |
| 3 | Look for any item labeled "Tips" in the sidebar. | "Tips" is NOT present anywhere in the sidebar. |
| 4 | Locate the "Settings" item and identify the item immediately below it. | The item immediately below "Settings" is labeled "Resources." |
| 5 | Confirm "Notifications" appears after "Resources." | Sidebar order: … Settings → Resources → Notifications … |

## Expected Final State

Sidebar order: … Settings → Resources → Notifications …

## Pass/Fail Criteria

**Pass:**
- "Tips" is completely absent from the sidebar
- "Resources" appears directly after "Settings"
- Sidebar order matches the expected sequence

**Fail:**
- "Tips" is still visible in the sidebar
- "Resources" is missing from the sidebar
- "Resources" appears in a position other than immediately after "Settings"
