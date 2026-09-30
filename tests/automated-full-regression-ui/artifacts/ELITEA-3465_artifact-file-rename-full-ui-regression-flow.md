---
id: ELITEA-3465
title: "Rename Artifact File — Full UI Regression Flow (E2E)"
priority: high
type: regression
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.7, comm:feedback, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#6438]
---

# ELITEA-3465: Rename Artifact File — Full UI Regression Flow (E2E)

**Module:** artifacts · **Priority:** high · **Type:** regression

**Objective:** Exercise all UI-observable artifact file rename behaviors in a single consolidated end-to-end regression pass — entry points, dialog states, client-side validation, happy path, conflict handling, and post-rename usability.

---

## Preconditions

- User is logged in to `{{base_url}}` with `artifacts.edit` permission on the target project/bucket.
- A private (or owned) project with an artifact bucket exists, pre-populated with at least:
  - One file (e.g. `Report.docx`) not currently open.
  - A second file whose name will be used as a "duplicate target" (e.g. `Existing.txt`).
- No other user is concurrently modifying the same bucket.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Root file to rename | `Report.docx` |
| Existing file (for duplicate-name negative test) | `Existing.txt` |
| New name with spaces/unicode/symbols | `Q3 Report Résumé (final)!.docx` |
| Unchanged-name test | `Report.docx` → `Report.docx` (rejected) |
| Empty name | `` (rejected) |
| Whitespace-only name | `   ` (trimmed → treated as empty, rejected) |
| Name containing slash | `Sub/Report.docx` (blocked client-side) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the artifact bucket table with some files already uploaded in it. | Table loads and displays the existing files. |
| 2 | Open the three-dot menu for any file. | Menu shows "Rename" with a pencil icon in between download and delete options |
| 3 | Select two or more files via multi-select and open the bulk toolbar. | Bulk toolbar does NOT offer "Rename" (single-file only feature). |
| 4 | From the file row three-dot menu, click "Rename". | Dialog opens, pre-filled with the current base filename (no extension), input focused/selected. Extension is shown as a non-editable suffix next to the input; it cannot be changed in the UI dialog. |
| 5 | Clear the input completely. | "Rename" button becomes disabled. |
| 6 | Re-type the exact original name (unchanged) and submit. | Error "New name must be different from current name" is shown; no table change. |
| 7 | Enter only spaces into the input and attempt submit. | Input is treated as empty; submission is blocked. |
| 8 | Enter a name containing `/` (e.g. `Sub/Report`) and attempt submit. | Submission is blocked client-side; no request is sent. |
| 9 | Enter a valid new name and click "Cancel". | Dialog closes; no change to filename; no API call made. |
| 10 | Re-open Rename, enter a valid new name (`Q3-Report`), and press Enter (instead of clicking the button). | Same behavior as clicking "Rename" — request submits. |
| 11 | While the rename request is in flight, observe the dialog. | Input, Cancel, and Rename are disabled; button label shows "Renaming...". |
| 12 | Wait for completion. | Success message shown as "File has been successfully renamed."; table refreshes with new name; old name no longer present. |
| 13 | Attempt to rename the file to the name of the existing file `Existing.txt` (same extension collision scenario, adapted to available files). | Rename is blocked with "Destination file already exists: Existing.txt". |
| 14 | Open the renamed file's preview, open the preview header three-dot menu, click "Rename", submit a new valid name. | Rename succeeds; preview closes after the rename. |
| 15 | Rename a file to a name containing spaces, unicode characters, and symbols (`Q3 Report Résumé (final)!.docx`). | Rename succeeds; new name displays correctly in the table (no encoding/truncation issues). |
| 16 | Download, preview, and then delete the most recently renamed file. | All three actions succeed using the new filename. |
| 17 | Toggle light/dark theme and re-open the three-dot menu on a remaining file row. | Rename (and other) row action icons render correctly in both themes. |

## Expected Final State

All UI-observable Rename behaviors (entry points, dialog states, client-side validation, happy path, conflict handling, post-rename usability, and visual rendering) have been exercised end-to-end in a single pass without requiring separate isolated test runs.

## Pass/Fail Criteria

**Pass:**
- Every step's expected result is observed exactly as described.
- No unrelated UI regressions (broken table state, stuck loading spinners, orphaned dialogs) occur during the flow.

**Fail:**
- Any entry point shows/hides Rename incorrectly.
- Any client-side validation fails to block invalid input, or blocks valid input.
- The dialog does not reflect in-flight/disabled states correctly.
- Post-rename actions (download/preview/delete) fail on the renamed file.
