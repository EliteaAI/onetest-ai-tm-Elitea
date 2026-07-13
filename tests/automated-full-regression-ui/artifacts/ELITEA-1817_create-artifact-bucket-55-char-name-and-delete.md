---
id: ELITEA-1817
title: "Create Artifact Bucket with 55-Character Name and Delete It"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1817: Create Artifact Bucket with 55-Character Name and Delete It

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that a bucket with a 55-character name can be created without any character limit warning, and can be deleted via the actions menu with confirmation, resulting in removal from the bucket list.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name (55 chars) | bucket-a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4y |
| Retention policy | Years, 1 (default) |
| Delete confirmation message | Are you sure to delete bucket-a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4y? It can't be restored. |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click the folder/"create bucket" icon located above the bucket list | "New Bucket" form opens |
| 3 | Verify the "New Bucket" form opens | Form is visible |
| 4 | Enter the 55-character bucket name: "bucket-a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4y" | Name field accepts the full 55-character name |
| 5 | Verify no character limit warning is displayed | No character limit warning appears |
| 6 | Leave Retention policy as default (Years, 1) | Retention policy remains at default |
| 7 | Click "Save" | Bucket is saved |
| 8 | Verify bucket "bucket-a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4y" appears in the bucket list | Bucket is listed |
| 9 | Click the 3-dot (ellipsis) / actions icon next to the bucket in the bucket list | Dropdown menu appears |
| 10 | Verify a dropdown menu appears with options: "Upload files", "Pin to top", "Edit", "Delete" | All four options are visible |
| 11 | Click "Delete" | Delete confirmation modal opens |
| 12 | Verify a "Delete confirmation" modal opens with the correct message and "Cancel" and "Delete" buttons | Modal shows correct message with both buttons |
| 13 | Click the "Delete" button in the modal | Deletion completes |
| 14 | Verify a success notification is displayed: "The bucket has been deleted successfully" | Success notification appears |
| 15 | Verify the bucket is no longer listed in the bucket list | Bucket is removed from the list |

---

## Expected Final State

The 55-character bucket is created without any warnings, then successfully deleted with a confirmation modal. The bucket is no longer listed after deletion.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Bucket is created without character limit warning and deleted successfully.

**Fail:**
- Any step produces an error or unexpected result.
- Character limit warning appears for 55 chars, or bucket cannot be deleted.
