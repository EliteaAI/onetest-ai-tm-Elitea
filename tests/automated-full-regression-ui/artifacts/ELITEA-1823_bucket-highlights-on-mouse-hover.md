---
id: ELITEA-1823
title: "Bucket Highlights on Mouse Hover"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1823: Bucket Highlights on Mouse Hover

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that hovering the mouse cursor over a bucket row changes its visual appearance (highlight), and that only the bucket currently under the cursor is highlighted at any time.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least two buckets are present in the bucket list.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Verify the bucket list is displayed with at least one bucket present | Bucket list is visible |
| 3 | Move the mouse cursor away from the bucket list | No bucket is highlighted |
| 4 | Slowly move the mouse cursor over the first bucket in the list | Bucket row background color changes to indicate highlight |
| 5 | Verify the bucket row becomes visually highlighted (background colour changes) when the cursor hovers over it | First bucket is highlighted |
| 6 | Move the mouse cursor to the next bucket in the list | Cursor moves to the next bucket |
| 7 | Verify the previously hovered bucket returns to its default appearance and the newly hovered bucket becomes highlighted | Only the current bucket is highlighted; previous bucket returns to default |
| 8 | Repeat for several buckets in the list — verify only the bucket currently under the cursor is highlighted at any time | Single-bucket highlight is consistent across the list |

---

## Expected Final State

Hover highlighting behaves correctly: only one bucket is highlighted at a time (the one under the cursor), and the highlight is removed when the cursor moves away.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Hover highlight applies to only the bucket under the cursor and reverts correctly.

**Fail:**
- Any step produces an error or unexpected result.
- No highlight on hover, multiple buckets highlighted simultaneously, or highlight does not revert.
