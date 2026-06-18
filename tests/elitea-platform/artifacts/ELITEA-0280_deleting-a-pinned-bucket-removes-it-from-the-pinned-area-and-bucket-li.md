---
id: ELITEA-0280
title: "Deleting a pinned bucket removes it from the pinned area and bucket list without leaving broken references"
priority: critical
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, r-2.0.3, 4180]
requirements: [EliteaAI/elitea_issues#4180]
---
# ELITEA-0280: Deleting a pinned bucket removes it from the pinned area and bucket list without leaving broken references

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a pinned bucket is deleted, it is fully removed from both the pinned position at the top and the regular bucket list, with no ghost entries or broken references remaining.

**Coverage:**
- Pinned bucket is fully removed from the pinned area on deletion
- No ghost or broken reference entry remains at the top of the sidebar
- Bucket is also absent from the regular bucket list after deletion
- System auto-selects the next available bucket correctly
- No JavaScript errors or failed API requests after deletion

## Preconditions

- Logged in to ELITEA ({{base_url}}
- A dedicated test bucket exists and can be safely deleted
- User has `artifacts.buckets.delete` permission or is bucket owner

## Test Data

- Test bucket for deletion: `test-pin-delete-bucket` (create if it does not exist)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the left sidebar. | Artifacts page opens. |
| 2 | Pin the test bucket `test-pin-delete-bucket` via its ⋮ context menu → 'Pin to top'. | Bucket appears at the top with 📌 icon. |
| 3 | Hover over the pinned test bucket and click ⋮. | Context menu appears with 'Upload files', 'Unpin from top', 'Edit', 'Delete'. |
| 4 | Click 'Delete'. | Confirmation dialog appears asking to confirm permanent deletion. |
| 5 | Click 'Delete' in the confirmation dialog. | Dialog closes; deletion is processed. |
| 6 | Observe the top of the bucket sidebar. | No entry for `test-pin-delete-bucket` remains in the pinned area — no ghost or broken reference. |
| 7 | Observe the full bucket list below the pinned group. | `test-pin-delete-bucket` is also absent from the regular bucket list. |
| 8 | Observe the auto-selected bucket. | System automatically selects the next available bucket; no 'undefined' or blank state. |
| 9 | Open browser DevTools console (F12) and check for errors. | No JavaScript errors or failed API requests in the console. |

## Expected Final State

No JavaScript errors or failed API requests in the console.

## Pass/Fail Criteria

**Pass:**
- Deleted bucket absent from both pinned area and regular list
- No ghost or broken reference remains
- Auto-selection switches to next available bucket correctly
- No console errors or error toasts appear

**Fail:**
- Ghost entry remains at top after deletion
- Bucket still appears in the regular list after deletion
- Auto-selection shows blank or undefined state
- Console errors or failed API requests are present
