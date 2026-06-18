---
id: ELITEA-0282
title: "Unpin a bucket via context menu \"Unpin from top\" and verify position and icon revert"
priority: critical
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, r-2.0.3, 4180]
requirements: [EliteaAI/elitea_issues#4180]
---
# ELITEA-0282: Unpin a bucket via context menu "Unpin from top" and verify position and icon revert

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking "Unpin from top" in the context menu moves the bucket back to the regular list and reverts the pin icon to its default (non-filled) state.

**Coverage:**
- "Unpin from top" is present in the ⋮ context menu for a pinned bucket
- Bucket moves back below all pinned buckets into the regular list after unpinning
- Pin icon reverts to no-icon or hover-only outline state
- Context menu switches back to "Pin to top"

## Preconditions

- Logged in to ELITEA ({{base_url}}
- At least one bucket is currently pinned and visible at the top of the bucket sidebar

## Test Data

- Any currently pinned bucket

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the left sidebar. | Artifacts page opens; at least one bucket is pinned at the top with 📌 icon. |
| 2 | Hover over the pinned bucket at the top of the sidebar. | The ⋮ icon appears on the pinned bucket row. |
| 3 | Click the ⋮ icon to open the context menu. | Context menu appears showing 'Unpin from top' (not 'Pin to top'). |
| 4 | Click 'Unpin from top'. | Context menu closes; bucket moves out of the pinned position into the regular bucket list. |
| 5 | Observe the bucket's pin icon in its new position. | No filled 📌 icon is displayed; icon is absent or shows only on hover as an outline. |
| 6 | Hover over the now-unpinned bucket. | Outline/empty pin icon appears on hover. |
| 7 | Move cursor away from the bucket. | The hover pin icon disappears again. |
| 8 | Click ⋮ on the now-unpinned bucket. | Context menu shows 'Pin to top' again. |

## Expected Final State

Context menu shows 'Pin to top' again.

## Pass/Fail Criteria

**Pass:**
- Bucket returns to regular list
- Filled icon removed from unpinned bucket
- Context menu shows 'Pin to top' after unpinning
- No error toasts appear

**Fail:**
- Bucket stays at top after unpinning
- Icon remains filled after unpinning
- Context menu still shows 'Unpin from top'
- Error toast or console error appears
