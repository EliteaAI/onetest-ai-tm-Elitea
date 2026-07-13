---
id: ELITEA-1815
title: "Save and Cancel Buttons Active with Valid Values; Cancel Does Not Create Bucket"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1815: Save and Cancel Buttons Active with Valid Values; Cancel Does Not Create Bucket

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that both Save and Cancel buttons are visible and active when a valid bucket name and retention policy are provided, and that clicking Cancel closes the form without creating the bucket.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-cancel-test |
| Retention policy | days |
| Retention value | 3 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section | Artifacts page loads |
| 2 | Click the folder/"create bucket" icon located above the bucket list | "New Bucket" form opens |
| 3 | Enter a valid bucket name: "bucket-cancel-test" | Name field accepts "bucket-cancel-test" |
| 4 | Select retention policy: "days" from the dropdown | "days" is selected |
| 5 | Set the retention numerical field to: "3" | Numerical field shows "3" |
| 6 | Verify both the "Save" button (highlighted/active) and "Cancel" button are visible, active and clickable | Both buttons are visible and active |
| 7 | Click "Cancel" | Form closes |
| 8 | Click to "Artifacts" | Navigation to Artifacts root occurs |
| 9 | Verify "bucket-cancel-test" does NOT appear in the bucket list | "bucket-cancel-test" is absent from the list |

---

## Expected Final State

No bucket named "bucket-cancel-test" is created. Both buttons are active when valid values are filled in, and Cancel closes the form without any side effects.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Both buttons are active with valid values; Cancel closes the form and no bucket is created.

**Fail:**
- Any step produces an error or unexpected result.
- Save or Cancel button is disabled with valid inputs, or bucket is created after Cancel.
