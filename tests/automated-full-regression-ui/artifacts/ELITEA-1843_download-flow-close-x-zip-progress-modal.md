---
id: ELITEA-1843
title: "Download Flow – Close X Button on ZIP Progress Modal Cancels Download"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1843: Download Flow – Close X Button on ZIP Progress Modal Cancels Download

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking the X (close) button on the ZIP progress modal stops the download, closes the modal, and displays a "Download cancelled" notification.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" with subfolder "a1" contains at least 3 files for download.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Subfolder | a1 |
| Cancellation notification | Download cancelled |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" and navigate to subfolder "a1" | Subfolder "a1" is selected |
| 3 | Select 3 or more files using their checkboxes | Files are selected |
| 4 | Click the "Download files" icon in the top-right of the main panel | ZIP preparation progress modal opens |
| 5 | Verify the "Preparing bucket-1.zip" progress modal opens and the download begins | Modal is visible and progress starts |
| 6 | Click the X (close) icon in the top-right corner of the progress modal | Modal closes |
| 7 | Verify the progress modal closes immediately | Modal is no longer visible |
| 8 | Verify a notification is displayed: "Download cancelled" | "Download cancelled" notification appears |
| 9 | Verify no ZIP file is saved to the local machine | No ZIP file in downloads |

---

## Expected Final State

Clicking X on the progress modal cancels the download, closes the modal, and shows a "Download cancelled" notification. No ZIP file is saved.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Modal closes via X; "Download cancelled" notification shown; no ZIP saved.

**Fail:**
- Any step produces an error or unexpected result.
- ZIP file is saved after closing via X, or notification does not appear.
