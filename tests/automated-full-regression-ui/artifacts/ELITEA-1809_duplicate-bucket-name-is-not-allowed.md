---
id: ELITEA-1809
title: "Duplicate Bucket Name Is Not Allowed"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1809: Duplicate Bucket Name Is Not Allowed

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that attempting to create a bucket with the same name as an existing bucket results in an error notification, the form remains open, and no duplicate bucket is created.

---

## Preconditions

- User is logged in to the Elitea platform.
- A bucket named "bucket-1" already exists in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Existing bucket name | bucket-1 |
| Search keyword | buck |
| Error message | Bucket with name bucket-1 already exists |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click the search (magnifier/loop) icon next to the "BUCKETS" label in the left panel header | Search input field opens with tooltip "Search buckets" |
| 3 | Verify a search input field opens with a tooltip "Search buckets" | Search field is visible with correct tooltip |
| 4 | Enter "buck" in the search field | Bucket list filters to show matching results |
| 5 | Verify the bucket list filters and displays only buckets whose names contain "buck" | Only buckets with "buck" in their name are shown |
| 6 | Verify that "bucket-1" is present in the filtered results | "bucket-1" is listed |
| 7 | Clear the search field and close the search box | Search is closed and full bucket list is restored |
| 8 | Click the folder/"create bucket" icon located above the bucket list | "New Bucket" form opens |
| 9 | Verify the "New Bucket" form opens | Form is visible |
| 10 | Enter bucket name: "bucket-1" (same name as the existing bucket) | Name field displays "bucket-1" |
| 11 | Leave Retention policy as default (Years, 1) | Retention policy remains at default |
| 12 | Click "Save" | Save is attempted |
| 13 | Verify an error notification is displayed in red: "Bucket with name bucket-1 already exists" | Red error notification is displayed with the correct message |
| 14 | Verify the "New Bucket" form remains open | Form is still visible and not closed |
| 15 | Click "Artifacts" | Navigation to Artifacts root occurs |
| 16 | Click the search icon again and enter "buck" in the search field | Search filters the bucket list |
| 17 | Verify the filtered bucket list does not contain a duplicate entry of "bucket-1" | Only one "bucket-1" entry is shown |
| 18 | Verify only one "bucket-1" is present in the filtered results | No duplicate bucket was created |

---

## Expected Final State

Only one "bucket-1" exists in the bucket list. The duplicate creation attempt is blocked with an error notification and the form remains open.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Error notification is shown for duplicate name, form remains open, no duplicate bucket is created.

**Fail:**
- Any step produces an error or unexpected result.
- A duplicate bucket is created, or the error notification is not displayed.
