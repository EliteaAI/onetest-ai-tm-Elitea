---
id: ELITEA-0276
title: "Pinning multiple buckets keeps all pinned buckets grouped at the top above unpinned buckets"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, r-2.0.3, 4180]
requirements: [EliteaAI/elitea_issues#4180]
---
# ELITEA-0276: Pinning multiple buckets keeps all pinned buckets grouped at the top above unpinned buckets

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that multiple pinned buckets consistently appear above all unpinned buckets in the sidebar, and that unpinning one from the group does not affect the position of others.

**Coverage:**
- Pinning 3 buckets in sequence groups all 3 at the top with 📌 icons
- All unpinned buckets remain below the pinned group
- Unpinning one bucket from the group returns only that bucket to the regular list
- Remaining pinned buckets stay in their pinned positions undisturbed

## Preconditions

- Logged in to ELITEA ({{base_url}}
- At least 4 buckets are available (3 to pin, 1 to remain unpinned)
- No buckets are currently pinned

## Test Data

- Buckets to pin: e.g., `a`, `A`, `a1` (or any 3 available buckets)
- Bucket to leave unpinned: e.g., `a11`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the left sidebar. | Bucket sidebar is visible; no buckets are pinned. |
| 2 | Pin bucket `a` via ⋮ → 'Pin to top'. | `a` moves to top with 📌 icon. |
| 3 | Pin bucket `A` via ⋮ → 'Pin to top'. | `A` also appears in the pinned group at top; `a` remains pinned. |
| 4 | Pin bucket `a1` via ⋮ → 'Pin to top'. | `a1` joins the pinned group; all 3 pinned buckets are at the top with 📌 icons. |
| 5 | Verify all unpinned buckets are below the pinned group. | No unpinned bucket appears between or above the pinned buckets. |
| 6 | Unpin bucket `A` via ⋮ → 'Unpin from top'. | `A` moves below the pinned group into the regular list. |
| 7 | Verify `a` and `a1` remain in the pinned group at the top with 📌 icons. | `a` and `a1` are still at the top; `A` is now in the regular section. |

## Expected Final State

`a` and `a1` are still at the top; `A` is now in the regular section.

## Pass/Fail Criteria

**Pass:**
- All pinned buckets are grouped at the top
- Unpinned buckets remain below the pinned group
- Unpinning one bucket does not affect others in the pinned group
- Icons are correct on all buckets

**Fail:**
- Unpinned buckets appear intermixed with pinned ones
- Unpinning one bucket removes others from their pinned position
- Icons are incorrect or inconsistent
