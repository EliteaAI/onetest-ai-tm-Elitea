---
id: ELITEA-2787
title: "Index Details - Configuration and Activity Tabs"
priority: high
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, indexes, configuration, activity]
requirements: []
---
# ELITEA-2787: Index Details - Configuration and Activity Tabs

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify Configuration and Activity tabs functionality on Index Details page.

**Coverage:**
- Configuration tab shows index settings
- Activity tab shows indexing log
- Reindex button triggers reindexing
- Tab switching works correctly

## Preconditions

- Logged in to {{base_url}}
- A toolkit with at least one completed index

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with indexes |
| Index | A completed index |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → select toolkit → click an index card. | Index details page opens. |
| 2 | Observe the right panel tabs. | "Configuration" and "Activity" tabs visible; Configuration is default/active. |
| 3 | In Configuration tab, verify displayed information. | Shows Branch, Whitelist, Blacklist settings (if configured). |
| 4 | Click the "Activity" tab. | Activity panel opens. |
| 5 | Observe the Activity tab content. | Shows indexing activity log or "No indexing activity" if idle. |
| 6 | Click the "Configuration" tab to switch back. | Configuration panel displays. |
| 7 | Click the "Reindex" button at bottom of page. | Reindex operation starts; Activity tab may update with new activity. |
| 8 | Switch to Activity tab during/after reindex. | Activity log shows reindexing progress or completion message. |

## Expected Final State

Both tabs function correctly, showing appropriate content for Configuration (settings) and Activity (logs).

## Pass/Fail Criteria

**Pass:**
- Configuration tab shows index settings
- Activity tab shows indexing logs
- Tab switching is smooth
- Reindex triggers new activity

**Fail:**
- Tabs don't switch or show wrong content
- Configuration missing index settings
- Activity doesn't show logs
- Reindex doesn't trigger
