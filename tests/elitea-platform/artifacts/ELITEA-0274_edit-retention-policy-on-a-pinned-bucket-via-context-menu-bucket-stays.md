---
id: ELITEA-0274
title: "Edit retention policy on a pinned bucket via context menu — bucket stays pinned and name is read-only"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, r-2.0.3, 4180]
requirements: [EliteaAI/elitea_issues#4180]
---
# ELITEA-0274: Edit retention policy on a pinned bucket via context menu — bucket stays pinned and name is read-only

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that the "Edit" context menu option on a pinned bucket still correctly opens the Edit Bucket dialog, allows modifying the retention policy, saves successfully, and keeps the bucket pinned — and that the bucket name field is non-editable.

**Coverage:**
- Edit dialog opens from the ⋮ context menu on a pinned bucket
- Bucket name field is read-only in edit mode (renaming is not supported)
- Retention policy (Period Type and Value) can be modified and saved
- Bucket remains pinned at the top after saving retention changes
- No error toasts appear during the edit operation

## Preconditions

- Logged in to ELITEA ({{base_url}}
- At least one bucket is pinned
- User has `artifacts.buckets.update` permission or is bucket owner

## Test Data

- Pinned bucket: any pinned bucket
- New retention policy: change Period Type (e.g., `Days` → `Weeks`) or value (e.g., `30`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the left sidebar. | Bucket sidebar shows at least one pinned bucket with 📌 icon. |
| 2 | Click ⋮ on the pinned bucket. | Context menu appears: 'Upload files', 'Unpin from top', 'Edit', 'Delete'. |
| 3 | Click 'Edit'. | The 'Edit Bucket' dialog opens. |
| 4 | Observe the bucket name field. | The name field is read-only / non-editable (bucket renaming is not supported). |
| 5 | Modify the retention policy (Period Type and/or Value). | Changes are reflected in the dialog fields. |
| 6 | Click 'Save'. | Dialog closes; no error toast appears. |
| 7 | Verify the bucket is still pinned at the top with 📌 icon. | Bucket remains in the pinned position with the filled pin icon. |

## Expected Final State

Bucket remains in the pinned position with the filled pin icon.

## Pass/Fail Criteria

**Pass:**
- Edit dialog opens correctly for a pinned bucket
- Bucket name field is read-only
- Retention policy saves without errors
- Bucket remains pinned at the top after saving

**Fail:**
- Edit dialog does not open from the context menu
- Bucket name field is editable
- Save triggers an error toast
- Bucket becomes unpinned after saving
