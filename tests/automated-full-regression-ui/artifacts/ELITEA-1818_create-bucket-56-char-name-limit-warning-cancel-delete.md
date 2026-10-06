---
id: ELITEA-1818
title: "Create Artifact Bucket with 56-Character Name and Verify Limit Warning and Delete Cancellation"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1818: Create Artifact Bucket with 56-Character Name and Verify Limit Warning and Delete Cancellation

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that a bucket with a 56-character name triggers a character limit warning, can still be created, and that clicking Cancel on the delete confirmation keeps the bucket intact.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name (56 chars) | bucket-a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4y5 |
| Character limit warning | 0 of 56 remaining |
| Retention policy | Years, 1 (default) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click the folder/"create bucket" icon located above the bucket list | "New Bucket" form opens |
| 3 | Verify the "New Bucket" form opens | Form is visible |
| 4 | Enter the 56-character bucket name: "bucket-a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4y5" | Name field accepts the full 56-character name |
| 5 | Verify a character limit warning is displayed indicating "0 of 56 remaining" below the name field | Character limit warning "0 of 56 remaining" is shown |
| 6 | Leave Retention policy as default (Years, 1) | Retention policy remains at default |
| 7 | Click "Save" | Bucket is saved |
| 8 | Verify bucket "bucket-a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4y5" appears in the bucket list | Bucket is listed |
| 9 | Click the 3-dot (ellipsis) / actions icon next to the bucket in the bucket list | Dropdown menu appears |
| 10 | Verify a dropdown menu appears with options: "Upload files", "Pin to top", "Edit", "Delete" | All four options are visible |
| 11 | Click "Delete" | Delete confirmation modal opens |
| 12 | Verify a "Delete confirmation" modal opens with the correct message and "Cancel" and "Delete" buttons | Modal is displayed with correct message |
| 13 | Click the "Cancel" button in the modal | Modal closes without deletion |
| 14 | Verify the "Delete confirmation" modal is closed | Modal is no longer visible |
| 15 | Verify the bucket is still listed in the bucket list and was not deleted | Bucket remains in the list |

---

## Expected Final State

The 56-character bucket shows the character limit warning at creation, is successfully created, and clicking Cancel on the delete confirmation keeps the bucket intact.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Character limit warning shown at 56 chars, bucket created, Cancel on delete keeps bucket.

**Fail:**
- Any step produces an error or unexpected result.
- Character limit warning is absent at 56 chars, or Cancel deletes the bucket.
