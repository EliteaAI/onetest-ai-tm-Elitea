---
id: ELITEA-1820
title: "Pin and Unpin Artifact Bucket to/from Top"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1820: Pin and Unpin Artifact Bucket to/from Top

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that a bucket can be pinned to the top of the bucket list via "Pin to top", and subsequently unpinned via "Unpin from top", with the pin icon and list position updating correctly in both directions.

---

## Preconditions

- User is logged in to the Elitea platform.
- The bucket list contains at least two buckets displayed in alphanumeric order.
- "bucket-1" exists and is not currently at the top of the list.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket to pin/unpin | bucket-1 |

---

## Steps

### Part 1: Pin to Top

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Verify the bucket list is displayed in alphanumeric order | Bucket list is in alphanumeric order |
| 3 | Identify a bucket that is not currently at the top of the list (e.g. "bucket-1") | "bucket-1" is not the first item |
| 4 | Hover over "bucket-1" to reveal the 3-dot (ellipsis) / actions icon next to the bucket name | Actions icon becomes visible on hover |
| 5 | Click the 3-dot (ellipsis) / actions icon | Dropdown menu appears |
| 6 | Verify a dropdown menu appears with options: "Upload files", "Pin to top", "Edit", "Delete" | All four options are visible |
| 7 | Click "Pin to top" | Pin action completes |
| 8 | Verify a pin icon appears next to the bucket name "bucket-1" in the bucket list | Pin icon is visible next to "bucket-1" |
| 9 | Verify "bucket-1" is now displayed at the top of the bucket list above all unpinned buckets | "bucket-1" is the first item in the list |

### Part 2: Unpin from Top

| # | Action | Expected Result |
|---|--------|-----------------|
| 10 | Verify that "bucket-1" is still pinned and displayed at the top of the bucket list with a pin icon next to its name | "bucket-1" is at the top with pin icon |
| 11 | Click the 3-dot (ellipsis) / actions icon next to "bucket-1" | Dropdown menu appears |
| 12 | Verify a dropdown menu appears with options: "Upload files", "Unpin from top", "Edit", "Delete" | "Unpin from top" option is visible |
| 13 | Click "Unpin from top" | Unpin action completes |
| 14 | Verify the pin icon is no longer displayed next to "bucket-1" | Pin icon is removed |
| 15 | Verify "bucket-1" is no longer at the top of the bucket list | "bucket-1" is not the first item |
| 16 | Verify "bucket-1" is repositioned in the bucket list according to its correct alphanumeric order among the other unpinned buckets | "bucket-1" is in its correct alphabetical position |

---

## Expected Final State

"bucket-1" can be pinned to the top (with pin icon shown and list repositioned) and subsequently unpinned (pin icon removed and bucket returns to correct alphanumeric order).

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Pin icon appears and bucket moves to the top when pinned.
- Pin icon is removed and bucket returns to correct alphanumeric order when unpinned.

**Fail:**
- Any step produces an error or unexpected result.
- Pin icon does not appear/disappear correctly, or bucket position does not update as expected.

---

## Notes

**Source functional tests:** ELITEA-1820, ELITEA-1821

**Regression rationale:** Pin and Unpin are inverse actions on the same feature; consolidating into one pin→verify→unpin→verify flow avoids duplicated navigation/setup while preserving both checkpoints.

**Selected checkpoints:**
- Pin to top moves bucket to top with pin icon (ELITEA-1820)
- Unpin from top removes pin icon and restores alphanumeric position (ELITEA-1821)
