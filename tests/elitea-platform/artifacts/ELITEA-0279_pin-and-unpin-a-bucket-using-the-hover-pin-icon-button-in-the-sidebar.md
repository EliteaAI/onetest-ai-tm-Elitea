---
id: ELITEA-0279
title: "Pin and unpin a bucket using the hover pin icon button in the sidebar"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, r-2.0.3, 4180]
requirements: [EliteaAI/elitea_issues#4180]
---
# ELITEA-0279: Pin and unpin a bucket using the hover pin icon button in the sidebar

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that the pin icon appearing on hover next to a bucket name functions as an alternative control to pin or unpin a bucket.

**Coverage:**
- Outline pin icon appears on hover over an unpinned bucket
- Clicking the hover icon pins the bucket (moves to top, icon becomes filled)
- Filled pin icon is persistently visible on pinned bucket (not only on hover)
- Clicking the filled icon on a pinned bucket unpins it
- Bucket returns to regular list and icon reverts after unpinning

## Preconditions

- Logged in to ELITEA ({{base_url}}
- At least one unpinned bucket exists in the Artifacts sidebar

## Test Data

- Any unpinned bucket in the Artifacts sidebar

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the left sidebar. | Bucket sidebar is visible with a list of unpinned buckets. |
| 2 | Hover over an unpinned bucket in the sidebar. | An outline/empty pin icon appears on the bucket row. |
| 3 | Move the cursor away from the bucket. | The pin icon disappears; bucket row returns to default appearance. |
| 4 | Hover over the same unpinned bucket again. | Outline pin icon reappears on hover. |
| 5 | Click the outline pin icon. | Bucket moves to the top of the sidebar; pin icon becomes filled/solid 📌. |
| 6 | Move cursor away from the now-pinned bucket. | Filled 📌 icon remains visible without hover (persistent state for pinned buckets). |
| 7 | Hover over the pinned bucket at the top. | The filled icon remains; no change on hover. |
| 8 | Click the filled 📌 pin icon on the pinned bucket. | Bucket unpins; moves back to the regular list below. |
| 9 | Hover over the bucket in its new (unpinned) position. | Outline pin icon appears on hover; moving away makes it disappear. |

## Expected Final State

Outline pin icon appears on hover; moving away makes it disappear.

## Pass/Fail Criteria

**Pass:**
- Hover pin icon controls pin/unpin correctly
- Filled icon is persistent for pinned buckets (no hover required)
- Outline icon is hover-only for unpinned buckets
- No errors during any interaction

**Fail:**
- Hover icon does not appear on unpinned buckets
- Clicking icon has no effect
- Icon state does not match the actual pin state
- Errors appear during interaction
