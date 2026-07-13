---
id: ELITEA-1813
title: "Bucket Cannot Be Created with an Empty Name Field"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1813: Bucket Cannot Be Created with an Empty Name Field

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that the "Save" button is disabled and an inline validation message is displayed when the bucket Name field is empty, and that clicking Cancel closes the form without creating a bucket.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Default name in field | new-bucket |
| Validation message | Name is required |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click the folder/create icon located above the bucket list | "New Bucket" form opens |
| 3 | Delete the Name field default "new-bucket" name | Name field is cleared and empty |
| 4 | Verify the "Save" button is disabled / not clickable | "Save" button appears disabled |
| 5 | Verify an inline validation message is displayed: "Name is required" | Inline message "Name is required" is visible |
| 6 | Verify "Cancel" button is active and clickable | "Cancel" button is enabled |
| 7 | Click the "Cancel" button | Form closes |
| 8 | Verify bucket creation page is closed | Form is no longer visible |
| 9 | Verify bucket list is displayed and no new bucket is created | No new bucket appears in the bucket list |

---

## Expected Final State

No bucket is created. When the Name field is empty, the Save button is disabled and the "Name is required" validation message is shown. Clicking Cancel closes the form cleanly.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Save button is disabled, validation message is shown, and no bucket is created after Cancel.

**Fail:**
- Any step produces an error or unexpected result.
- Save button remains active with empty name, or a bucket is inadvertently created.
