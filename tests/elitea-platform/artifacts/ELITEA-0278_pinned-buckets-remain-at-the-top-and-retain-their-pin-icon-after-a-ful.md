---
id: ELITEA-0278
title: "Pinned buckets remain at the top and retain their pin icon after a full page refresh"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, r-2.0.3, 4180]
requirements: [EliteaAI/elitea_issues#4180]
---
# ELITEA-0278: Pinned buckets remain at the top and retain their pin icon after a full page refresh

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that pinned bucket state is persisted server-side and survives a browser page refresh, confirming it is not stored only in memory.

**Coverage:**
- Pinned buckets remain at the top of the bucket sidebar after full page refresh
- Each pinned bucket still shows the filled 📌 icon after refresh
- Unpinned buckets remain below the pinned group after refresh
- Page loads without errors after refresh

## Preconditions

- Logged in to ELITEA ({{base_url}}
- At least 2 buckets available

## Test Data

- Pin at least 2 buckets before refreshing (e.g., `bucket-for-agent1` and `a`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the left sidebar. | Bucket sidebar is visible. |
| 2 | Pin 2 buckets via ⋮ → 'Pin to top' (e.g., `bucket-for-agent1` and `a`). | Both buckets move to the top with 📌 icons. |
| 3 | Note the names and order of the pinned buckets. | Buckets are confirmed visually at top. |
| 4 | Press F5 or click the browser Refresh button. | Page reloads completely. |
| 5 | Wait for the Artifacts page to fully load. | Artifacts page and bucket sidebar are displayed. |
| 6 | Observe the bucket sidebar. | Both previously pinned buckets are still at the top with 📌 icons. |
| 7 | Verify unpinned buckets remain below the pinned group. | No change in the relative ordering of unpinned buckets. |

## Expected Final State

No change in the relative ordering of unpinned buckets.

## Pass/Fail Criteria

**Pass:**
- Pinned buckets remain at top with correct filled icons after refresh
- State is fully preserved across the page reload
- Unpinned buckets remain in the correct position

**Fail:**
- Pinned buckets return to the regular list after refresh
- Pin icons reset to outline or absent after refresh
- Page shows a different bucket order than before refresh
