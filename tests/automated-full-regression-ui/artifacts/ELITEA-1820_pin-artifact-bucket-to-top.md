---
id: ELITEA-1820
title: "Pin Artifact Bucket to Top"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1820: Pin Artifact Bucket to Top

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that a bucket can be pinned to the top of the bucket list using the "Pin to top" option, resulting in a pin icon appearing next to the bucket name and the bucket being repositioned to the top.

---

## Preconditions

- User is logged in to the Elitea platform.
- The bucket list contains at least two buckets displayed in alphanumeric order.
- "bucket-1" exists and is not currently at the top of the list.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket to pin | bucket-1 |

---

## Steps

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

---

## Expected Final State

"bucket-1" is pinned to the top of the bucket list, a pin icon appears next to its name, and it is displayed above all unpinned buckets.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Pin icon appears and bucket moves to the top of the list.

**Fail:**
- Any step produces an error or unexpected result.
- Pin icon does not appear or bucket does not move to the top.
