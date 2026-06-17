---
id: ELITEA-0272
title: "No phantom pinned section or ghost header appears when zero buckets are pinned"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, r-2.0.3, 4180]
requirements: [EliteaAI/elitea_issues#4180]
---
# ELITEA-0272: No phantom pinned section or ghost header appears when zero buckets are pinned

**Module:** Artifacts · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when all buckets are unpinned, the sidebar shows a clean regular bucket list with no residual "pinned" section, divider, or empty slot at the top.

**Coverage:**
- No empty section, divider, or phantom header appears at the top of the bucket list when no buckets are pinned
- All buckets are displayed in the regular list sorted by recent activity
- No filled 📌 pin icon is visible on any bucket in zero-pinned state
- Hover pin icon (outline) is available for all buckets

## Preconditions

- Logged in to ELITEA ({{base_url}}
- All buckets are unpinned before starting (zero pinned buckets)

## Test Data

- Zero pinned buckets (ensure all are unpinned before testing)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts with all buckets unpinned (zero pinned buckets). | Bucket sidebar loads. |
| 2 | Observe the top of the bucket sidebar. | No empty section, divider line, 'Pinned Buckets' header, or blank slot appears at the top. |
| 3 | Verify all buckets display in the regular list. | Buckets are listed normally in sort order; no filled 📌 pin icon is visible on any bucket. |
| 4 | Hover over any bucket. | Outline hover pin icon appears; no filled icon exists. |

## Expected Final State

Outline hover pin icon appears; no filled icon exists.

## Pass/Fail Criteria

**Pass:**
- Clean sidebar with no phantom pinned section, divider, or ghost header
- All buckets displayed in the regular list
- No filled pin icons visible on any bucket

**Fail:**
- Empty section, divider line, or "Pinned Buckets" header remains at the top
- Ghost or blank slot appears at the top of the bucket sidebar
- Any bucket shows a filled pin icon unexpectedly
