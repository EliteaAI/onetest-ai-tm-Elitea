---
id: ELITEA-1863
title: "File Preview/Edit – Unsupported File Type (.xlsx) Shows Preview Not Available Message"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1863: File Preview/Edit – Unsupported File Type (.xlsx) Shows Preview Not Available Message

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking the "View/Edit file" icon for an unsupported .xlsx file displays the "Preview Not Available" message with supported formats info and a Download button, with Save/Discard buttons inactive.

---

## Preconditions

- User is logged in to the Elitea platform.
- A bucket contains "top-5-soccer-players.xlsx".

---

## Test Data

| Field | Value |
|-------|-------|
| File name | top-5-soccer-players.xlsx |
| Preview message | Preview Not Available |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section and locate a bucket containing "top-5-soccer-players.xlsx" | Bucket with file is found |
| 2 | Hover over the "top-5-soccer-players.xlsx" file row in the file table | "View/Edit file" icon appears on hover |
| 3 | Verify a "View/Edit file" (loop/magnifier) icon IS present on the row on hover | Icon is visible |
| 4 | Click the "View/Edit file" icon | Preview panel opens |
| 5 | Verify the file opens in the preview panel with the header displaying the file path (e.g. "epic/top-5-soccer-players.xlsx") | Header shows correct path |
| 6 | Verify the main content area displays an empty file icon and the message: "Preview Not Available" | "Preview Not Available" message is shown |
| 7 | Verify a supporting message is displayed listing the supported formats | Supported formats message is visible |
| 8 | Verify a "Download" button is displayed in the center of the preview area | Download button is present |
| 9 | Verify the "Save" and "Discard" buttons in the top-right are INACTIVE/greyed out | Both buttons are disabled |
| 10 | Verify no "Preview" / "Raw" tabs are shown | No tabs are visible |
| 11 | Click the "Download" button — verify the file starts downloading to the local machine | File download initiates |

---

## Expected Final State

The preview panel shows "Preview Not Available" with supported formats info and a Download button. Save/Discard are inactive. No tabs are shown. Download button works.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- "Preview Not Available" shown; Download button works; Save/Discard inactive.

**Fail:**
- Any step produces an error or unexpected result.
- Preview content displayed for unsupported type, or Download button absent.
