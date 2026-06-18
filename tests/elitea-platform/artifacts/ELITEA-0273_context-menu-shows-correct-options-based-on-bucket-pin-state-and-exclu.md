---
id: ELITEA-0273
title: "Context menu shows correct options based on bucket pin state and excludes Rename and Share"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, r-2.0.3, 4180]
requirements: [EliteaAI/elitea_issues#4180]
---
# ELITEA-0273: Context menu shows correct options based on bucket pin state and excludes Rename and Share

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that the ⋮ context menu dynamically shows "Pin to top" or "Unpin from top" based on the bucket's current pin state, and confirms that Rename and Share options are never present.

**Coverage:**
- Unpinned bucket context menu: "Upload files", "Pin to top", "Edit", "Delete"
- Pinned bucket context menu: "Upload files", "Unpin from top", "Edit", "Delete"
- "Rename" is absent in both states
- "Share" is absent in both states
- Toggle between "Pin to top" and "Unpin from top" is dynamic and accurate

## Preconditions

- Logged in to ELITEA ({{base_url}}
- At least one unpinned bucket and one pinned bucket are available in the sidebar

## Test Data

- One unpinned bucket and one pinned bucket in the Artifacts sidebar

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the left sidebar. | Bucket sidebar is visible with both pinned and unpinned buckets. |
| 2 | Hover over an unpinned bucket and click ⋮. | Context menu opens. |
| 3 | Check the options for the unpinned bucket. | Menu shows exactly: 'Upload files', 'Pin to top', 'Edit', 'Delete'. 'Rename' and 'Share' are absent. 'Unpin from top' is absent. |
| 4 | Close the context menu (press Escape or click away). | Menu closes. |
| 5 | Hover over a pinned bucket and click ⋮. | Context menu opens. |
| 6 | Check the options for the pinned bucket. | Menu shows exactly: 'Upload files', 'Unpin from top', 'Edit', 'Delete'. 'Rename' and 'Share' are absent. 'Pin to top' is absent (replaced by 'Unpin from top'). |

## Expected Final State

Menu shows exactly: 'Upload files', 'Unpin from top', 'Edit', 'Delete'. 'Rename' and 'Share' are absent. 'Pin to top' is absent (replaced by 'Unpin from top').

## Pass/Fail Criteria

**Pass:**
- Correct options displayed for both pinned and unpinned states
- "Rename" and "Share" always absent regardless of pin state
- Toggle between "Pin to top" and "Unpin from top" works correctly

**Fail:**
- "Pin to top" present when bucket is already pinned
- "Unpin from top" present when bucket is not pinned
- "Rename" or "Share" visible in any state
