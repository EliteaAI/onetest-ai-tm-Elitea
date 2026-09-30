---
id: ELITEA-3468
title: "Artifact File Rename — Entry Points, Dialog Behavior, and Client-Side Validation"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.7, comm:feedback]
requirements: [EliteaAI/elitea_issues#6438]
---

# ELITEA-3468: Artifact File Rename — Entry Points, Dialog Behavior, and Client-Side Validation

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify where the artifact file rename action is exposed, how its dialog behaves, and that client-side validation correctly rejects invalid input before any API call.

---

## Preconditions

- User is logged in to `{{base_url}}` with `artifacts.edit` permission on a test bucket.
- Bucket contains at least one root-level file with a multi-part-looking name/extension (e.g. `Report.docx`) and one additional existing file (used both for the multi-select step and as a duplicate-name conflict target, e.g. `Existing.txt`).
- Ability to toggle the application's light/dark theme.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | `Report.docx` |
| Existing file (multi-select + duplicate-name target) | `Existing.txt` |
| New valid name | `Report-v2` |
| Unchanged-name input | `Report` (same as current base name) |
| Name matching an existing file | `Existing` (collides with `Existing.txt`) |
| Name containing slash | `Sub/Report` |
| Whitespace-only input | `   ` (three spaces) |
| Empty input | `` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the artifact bucket table. Click the three-dot menu on the file row for `Report.docx`. | Menu shows "Rename" with a pencil icon. |
| 2 | Open the preview for `Report.docx`, then click the three-dot menu in the preview header. | Menu shows "Rename" option. |
| 3 | Return to the table, select `Report.docx` and `Existing.txt` via checkboxes to trigger the bulk/multi-select toolbar. | The bulk toolbar does NOT offer a "Rename" action. |
| 4 | Click the three-dot menu on `Report.docx` and click "Rename". | Dialog opens; input is pre-filled with `Report` (base name, no extension), focused and text selected; `.docx` is shown as a non-editable suffix next to the input with no control to change it. |
| 5 | Clear the input field entirely. | "Rename" button becomes disabled. |
| 6 | Type `Report-v2` into the input and click "Cancel". | Dialog closes; no API call is made; filename remains `Report.docx`. |
| 7 | Re-open the dialog, type `Report-v2`, and press Enter. | Submission occurs (same as clicking "Rename"). |
| 8 | Immediately after submitting, inspect the dialog while the request is in flight, then wait for completion. | Input, Cancel, and Rename are disabled and the button label reads "Renaming..." while in flight; dialog then closes and the table shows the file renamed to `Report-v2.docx`. |
| 9 | Re-open Rename on `Report-v2.docx`. Clear the input completely and attempt to submit. | Submission is blocked before any API request is made; button is disabled. |
| 10 | Leave the input unchanged (same base name) and submit. | Error "New name must be different from current name" is shown. |
| 11 | Attempt to rename `Report-v2.docx` to `Existing` (colliding with the already-existing `Existing.txt`). | The attempt is submitted, then rejected with "Destination file already exists: Existing.txt"; no file is overwritten. |
| 12 | Type a name containing a slash (`Sub/Report`) and attempt to submit. | Client-side validation blocks submission; no API request is sent. |
| 13 | Clear the input and type only spaces, then attempt to submit. | Input is trimmed and treated as empty; submission is blocked. |
| 14 | Switch the application to light theme and open the three-dot menu on a file row; then switch to dark theme and repeat. | Rename (and other) row action icons render clearly and correctly in both themes. |

## Expected Final State

Rename is available only from the single-file row three-dot menu and the single-file preview header three-dot menu (absent from bulk actions); the dialog correctly pre-fills, keeps the extension display non-editable, manages button enabled/disabled and in-flight states, and supports both click and Enter submission; empty, unchanged, duplicate-name, slash-containing, and whitespace-only input are all rejected before or immediately upon submission; row action icons (including Rename) render correctly in both light and dark themes.

## Pass/Fail Criteria

**Pass:** All 14 observations match exactly.
**Fail:** Rename is shown in the bulk toolbar, or missing from a valid entry point; the extension becomes editable; empty input allows submission; Cancel triggers an API call; in-flight controls remain interactive; any invalid or duplicate-name input is accepted, or valid input is blocked; or any row action icon is missing/misrendered in either theme.
