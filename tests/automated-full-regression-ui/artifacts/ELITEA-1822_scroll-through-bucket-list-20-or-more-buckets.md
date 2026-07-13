---
id: ELITEA-1822
title: "Scroll Through Bucket List with 20 or More Buckets"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1822: Scroll Through Bucket List with 20 or More Buckets

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that a bucket list with 20 or more buckets is scrollable using both the mouse scroll wheel and keyboard arrow keys, allowing the user to navigate through the full list.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least 20 buckets exist in the project. If fewer, create "bucket-1" through "bucket-20" using the bucket creation flow.

---

## Test Data

| Field | Value |
|-------|-------|
| Minimum bucket count | 20 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Verify the bucket list is displayed — if fewer than 20 buckets exist, create buckets "bucket-1" through "bucket-20" | At least 20 buckets are present |
| 3 | Verify at least 20 buckets are present in the bucket list | 20 or more buckets are listed |
| 4 | Place the mouse cursor over the bucket list panel | Cursor is over the bucket list |
| 5 | Scroll down using the mouse scroll wheel | List scrolls down and buckets further in the list become visible |
| 6 | Continue scrolling down until the last bucket in the list is visible | All 20 buckets can be reached by scrolling |
| 7 | Scroll back up using the mouse scroll wheel | List scrolls up |
| 8 | Continue scrolling up until the first bucket in the list is visible | First bucket is at the top |
| 9 | Click into the bucket list panel and press the Down arrow key repeatedly | List scrolls down and buckets further in the list become visible |
| 10 | Press the Up arrow key repeatedly | List scrolls back up to the first listed bucket |

---

## Expected Final State

The bucket list with 20+ buckets is fully scrollable via both mouse scroll wheel and keyboard arrow keys in both directions.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Full list is scrollable via mouse wheel and keyboard, reaching first and last items.

**Fail:**
- Any step produces an error or unexpected result.
- List does not scroll, or items beyond the visible area are not reachable.
