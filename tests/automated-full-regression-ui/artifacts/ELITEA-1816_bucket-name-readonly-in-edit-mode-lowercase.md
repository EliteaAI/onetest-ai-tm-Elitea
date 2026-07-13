---
id: ELITEA-1816
title: "Bucket Name Is Read-Only in Edit Mode and Displayed in Lowercase After Creation"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1816: Bucket Name Is Read-Only in Edit Mode and Displayed in Lowercase After Creation

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that a bucket created with mixed-case name is stored in lowercase, that the Edit form correctly shows the lowercase name in a read-only field, and that the retention policy fields remain editable.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Input bucket name | BuCkEt-Mix |
| Expected stored name | bucket-mix |
| Retention policy | Days, 1 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click the folder/"create bucket" icon located above the bucket list | "New Bucket" form opens |
| 3 | Enter bucket name in mixed case: "BuCkEt-Mix" | Name field accepts the input |
| 4 | Click the Retention policy dropdown and select "Days" | "Days" is selected |
| 5 | In numerical retention field enter value: "1" | Numerical field shows "1" |
| 6 | Click "Save" | Bucket is saved |
| 7 | Verify the bucket appears in the bucket list as "bucket-mix" (all lowercase) | "bucket-mix" is listed in lowercase |
| 8 | Click the 3-dot (ellipsis) / actions icon next to "bucket-mix" in the bucket list | Dropdown menu appears |
| 9 | Verify a dropdown menu appears with options: "Upload files", "Pin to top", "Edit", "Delete" | All four options are visible |
| 10 | Click "Edit" | "Edit Bucket" form opens |
| 11 | Verify the "Edit Bucket" form opens | Form is visible |
| 12 | Verify the Name field displays "bucket-mix" | Name field shows "bucket-mix" |
| 13 | Verify the Retention policy is set to "Days" with numerical value "1" | Retention shows "Days" with value "1" |
| 14 | Attempt to click into the Name field and modify the value (e.g., try to type or delete characters) | No text cursor appears; no input is accepted |
| 15 | Verify the Name field is read-only and no changes can be made to it | Name field is read-only |
| 16 | Verify the Retention policy dropdown and numerical field remain editable | Retention fields are editable |
| 17 | Click "Cancel" to close the form without making changes | Form closes without saving changes |

---

## Expected Final State

Bucket "bucket-mix" is stored and displayed in lowercase. In Edit mode the Name field is read-only while retention policy fields remain editable.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Bucket name is stored in lowercase, Name field is read-only in Edit mode, and retention fields are editable.

**Fail:**
- Any step produces an error or unexpected result.
- Name field accepts edits in Edit mode, or bucket name is not converted to lowercase.
