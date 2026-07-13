---
id: ELITEA-1821
title: "Unpin Artifact Bucket from Top"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1821: Unpin Artifact Bucket from Top

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that a pinned bucket can be unpinned from the top of the list using the "Unpin from top" option, resulting in the pin icon being removed and the bucket being repositioned to its correct alphanumeric order.

---

## Preconditions

- User is logged in to the Elitea platform.
- "bucket-1" is pinned and displayed at the top of the bucket list with a pin icon next to its name.

---

## Test Data

| Field | Value |
|-------|-------|
| Pinned bucket | bucket-1 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Verify that "bucket-1" is pinned and displayed at the top of the bucket list with a pin icon next to its name | "bucket-1" is at the top with pin icon |
| 3 | Click the 3-dot (ellipsis) / actions icon next to "bucket-1" | Dropdown menu appears |
| 4 | Verify a dropdown menu appears with options: "Upload files", "Unpin from top", "Edit", "Delete" | "Unpin from top" option is visible |
| 5 | Click "Unpin from top" | Unpin action completes |
| 6 | Verify the pin icon is no longer displayed next to "bucket-1" | Pin icon is removed |
| 7 | Verify "bucket-1" is no longer at the top of the bucket list | "bucket-1" is not the first item |
| 8 | Verify "bucket-1" is repositioned in the bucket list according to its correct alphanumeric order among the other unpinned buckets | "bucket-1" is in its correct alphabetical position |

---

## Expected Final State

"bucket-1" is unpinned, its pin icon is removed, and it is repositioned in the bucket list according to alphanumeric order among unpinned buckets.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Pin icon is removed and bucket is repositioned correctly.

**Fail:**
- Any step produces an error or unexpected result.
- Pin icon remains, or bucket stays at the top after unpinning.
