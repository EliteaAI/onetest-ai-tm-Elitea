---
id: ELITEA-1810
title: "Create Artifact Bucket via Folder Icon (Path 2) and Verify Retention Policy Edit and Persistence"
priority: high
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1810: Create Artifact Bucket via Folder Icon (Path 2) and Verify Retention Policy Edit and Persistence

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify the second bucket creation path using the folder icon above the bucket list, create a bucket with a custom retention policy, edit the retention policy multiple times and confirm persistence, and verify that Cancel does not save changes.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-2 |
| Initial retention | 10 Months |
| Updated retention | 20 Weeks |
| Cancel retention | 1 Days (should not be saved) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click the folder/create icon located above the bucket list (second path) | "New Bucket" form opens |
| 3 | Verify the "New Bucket" form opens with Name field and Retention policy section | Form is visible with all required fields |
| 4 | Enter bucket name: "bucket-2" | Name field accepts "bucket-2" |
| 5 | Click the Retention policy dropdown (default shows "Years") | Dropdown opens with retention options |
| 6 | Select "Months" from the dropdown | "Months" is selected |
| 7 | Click the retention numerical input field and change the value to "10" | Numerical field shows "10" |
| 8 | Click "Save" | Bucket is saved successfully |
| 9 | Verify bucket "bucket-2" appears in the bucket list | "bucket-2" is listed |
| 10 | Note the bucket name and position/ID in the bucket list | Bucket position/ID is noted |
| 11 | Click on the 3-dot ellipsis menu next to "bucket-2" | Dropdown menu appears |
| 12 | Select "Edit" from the dropdown menu | Edit form opens |
| 13 | Verify that the retention policy is set to "10 Months" | Retention shows "10 Months" |
| 14 | Click the Retention policy dropdown and select "Weeks" | "Weeks" is selected |
| 15 | Change the numerical value to "20" | Numerical field shows "20" |
| 16 | Click "Save" | Changes are saved successfully |
| 17 | Verify that "bucket-2" is still listed in the bucket list under the same name and same position/ID | Bucket name and position are unchanged |
| 18 | Click on the 3-dot ellipsis menu next to "bucket-2" again | Dropdown menu appears |
| 19 | Select "Edit" | Edit form opens |
| 20 | Verify that the retention policy is now set to "20 Weeks" | Retention shows "20 Weeks" confirming save |
| 21 | Click the Retention policy dropdown and select "Days" | "Days" is selected |
| 22 | Set the numerical value to "1" | Numerical field shows "1" |
| 23 | Click "Cancel" | Edit form closes without saving |
| 24 | Navigate back to the bucket list | Bucket list is visible |
| 25 | Click on the 3-dot ellipsis menu next to "bucket-2" | Dropdown menu appears |
| 26 | Select "Edit" | Edit form opens |
| 27 | Verify that the retention policy has NOT changed and is still set to "20 Weeks" | Retention still shows "20 Weeks" confirming Cancel did not save |

---

## Expected Final State

Bucket "bucket-2" is created with the retention policy correctly persisting through multiple edits. The final retention policy is "20 Weeks". The Cancel action in step 23 did not overwrite the saved changes.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Retention policy persists correctly after each Save, and Cancel does not overwrite saved data.

**Fail:**
- Any step produces an error or unexpected result.
- Retention policy does not persist, Cancel saves changes, or bucket is not created.
