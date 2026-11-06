---
id: ELITEA-1863
title: "File Preview/Edit – Unsupported File Types Have No Preview (.xlsx shows 'Preview Not Available', .zip has no preview icon)"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1863: File Preview/Edit – Unsupported File Types Have No Preview (.xlsx shows 'Preview Not Available', .zip has no preview icon)

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that unsupported file types are handled consistently in the preview flow: a type that still shows a "View/Edit file" icon (.xlsx) opens to a "Preview Not Available" message with a Download button, while a type that offers no preview entry point at all (.zip) shows no "View/Edit file" icon on hover and exposes only Download/Delete in its actions dropdown.

---

## Preconditions

- User is logged in to the Elitea platform.
- A bucket contains "top-5-soccer-players.xlsx".
- Bucket "bucket-1" contains "new-file-storage.zip" (ZIP Archive, 230.0 KB).

---

## Test Data

| Field | Value |
|-------|-------|
| .xlsx file | top-5-soccer-players.xlsx |
| Preview message | Preview Not Available |
| Bucket name | bucket-1 |
| .zip file | new-file-storage.zip |
| .zip file type | ZIP Archive |
| .zip file size | 230.0 KB |

---

## Steps

### Part 1: .xlsx – "Preview Not Available" Message with Download Button

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

### Part 2: .zip – No Preview Icon, Actions Limited to Download/Delete

| # | Action | Expected Result |
|---|--------|-----------------|
| 12 | Navigate to the Artifacts section and click on "bucket-1" | Bucket is selected |
| 13 | Verify "new-file-storage.zip" (ZIP Archive, 230.0 KB) is listed in the file table | File is visible |
| 14 | Hover over the "new-file-storage.zip" file row | Only 3-dot actions icon appears; no View/Edit icon |
| 15 | Verify the "View/Edit file" (loop/magnifier) icon is NOT present on the row for this file type | View/Edit icon is absent |
| 16 | Verify only the 3-dot (ellipsis) actions icon is available on hover | Only actions icon is visible |
| 17 | Click the 3-dot actions icon | Dropdown menu appears |
| 18 | Verify the dropdown contains only "Download" and "Delete" — no preview or view/edit option | Only Download and Delete are present |
| 19 | Click "Download" — verify the ZIP file starts downloading to the local machine | ZIP file download initiates |

---

## Expected Final State

Both unsupported file-type handling paths work correctly: .xlsx shows "Preview Not Available" with a working Download button and inactive Save/Discard; .zip shows no View/Edit icon at all and its actions dropdown contains only Download and Delete. Both files download successfully.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- .xlsx: "Preview Not Available" shown; Download button works; Save/Discard inactive; no tabs.
- .zip: no View/Edit icon; actions limited to Download and Delete; download works.

**Fail:**
- Any step produces an error or unexpected result.
- Preview content displayed for either unsupported type, Download button absent/non-functional, or View/Edit icon or extra actions appear where they shouldn't.

---

## Notes

**Source functional tests:** ELITEA-1863, ELITEA-1864

**Regression rationale:** Both tests verify the same "unsupported file type in preview" feature on two branches of its handling (a type still offering a preview entry point that then shows a not-available message, vs. a type offering no preview entry point at all); consolidating avoids duplicated setup while preserving both checkpoints.

**Selected checkpoints:**
- .xlsx shows "Preview Not Available" with supported-formats info and working Download; Save/Discard inactive; no tabs (ELITEA-1863)
- .zip has no View/Edit icon on hover; actions dropdown limited to Download/Delete (ELITEA-1864)
