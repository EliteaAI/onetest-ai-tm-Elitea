---
id: ELITEA-0283
title: "Pin a bucket to top via context menu (⋮) and verify icon and position change"
priority: critical
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, r-2.0.3, 4180]
requirements: [EliteaAI/elitea_issues#4180]
---
# ELITEA-0283: Pin a bucket to top via context menu (⋮) and verify icon and position change

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking "Pin to top" in the context menu moves the bucket to the top of the sidebar list and updates the pin icon to its filled/active state.

**Coverage:**
- "Pin to top" option is present in the ⋮ context menu for an unpinned bucket
- Bucket moves to the top of the bucket list immediately after pinning
- Pin icon changes to filled 📌 state on the pinned bucket
- Context menu for the pinned bucket shows "Unpin from top" (not "Pin to top")
- "Rename" and "Share" options are absent from the context menu

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Project has at least 2 artifact buckets
- No buckets are currently pinned (clean state)

## Test Data

- Bucket to pin: any available bucket (e.g., `bucket-for-agent1`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the left sidebar. | Artifacts page opens; the bucket sidebar is visible on the left with a list of buckets. |
| 2 | Hover over any unpinned bucket in the sidebar. | The bucket row highlights and the ⋮ (three dots) icon appears. |
| 3 | Click the ⋮ icon to open the context menu. | Context menu appears with options: 'Upload files', 'Pin to top', 'Edit', 'Delete'. |
| 4 | Verify 'Rename' and 'Share' are absent from the context menu. | Only the expected 4 options are shown; 'Rename' and 'Share' are not present. |
| 5 | Click 'Pin to top'. | The context menu closes; the bucket immediately moves to the top of the sidebar list. |
| 6 | Observe the pin icon on the bucket now at the top. | The bucket displays a filled/solid 📌 pin icon. |
| 7 | Click the ⋮ icon on the newly pinned bucket. | Context menu shows 'Unpin from top' instead of 'Pin to top'; all other options remain. |

## Expected Final State

Context menu shows 'Unpin from top' instead of 'Pin to top'; all other options remain.

## Pass/Fail Criteria

**Pass:**
- Bucket moves to top immediately after clicking 'Pin to top'
- Filled 📌 pin icon is displayed on the pinned bucket
- Context menu switches to 'Unpin from top'
- 'Rename' and 'Share' are absent from the context menu

**Fail:**
- Bucket position unchanged after pinning
- Pin icon does not update to filled state
- Context menu still shows 'Pin to top' after pinning
- 'Rename' or 'Share' options are visible
- Any error toast appears
