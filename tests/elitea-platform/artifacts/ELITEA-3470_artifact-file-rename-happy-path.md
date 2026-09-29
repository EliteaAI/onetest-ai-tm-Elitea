---
id: ELITEA-3470
title: "Artifact File Rename — Happy Path via Row Menu and Preview Header, With Varied Naming"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.7, comm:feedback]
requirements: [EliteaAI/elitea_issues#6438]
---

# ELITEA-3470: Artifact File Rename — Happy Path via Row Menu and Preview Header, With Varied Naming

**Module:** artifacts · **Priority:** critical · **Type:** functional

**Objective:** Verify that renaming an artifact file succeeds from both the row menu and the preview header, supports varied naming (spaces, unicode, symbols), and leaves the renamed file fully usable.

---

## Preconditions

- User has `artifacts.edit` permission on a bucket containing at least three root-level files.

## Test Data

| File | Rename path | Original name | New name |
|---|---|---|---|
| A | Row three-dot menu | `Alpha.docx` | `Alpha-Renamed.docx` |
| B | Preview header three-dot menu | `Beta.txt` | `Beta-Renamed.txt` |
| C | Row three-dot menu (varied naming) | `Plain.docx` | `Q3 Report Résumé (final) — v2!.docx` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Rename `Alpha.docx` to `Alpha-Renamed.docx` via the row three-dot menu. | Success message shown; table refreshes; `Alpha-Renamed.docx` is present, `Alpha.docx` is gone. |
| 2 | Open the preview of `Beta.txt`, rename it to `Beta-Renamed.txt` via the preview header three-dot menu. | Rename succeeds; the preview closes automatically after the rename completes. |
| 3 | Rename `Plain.docx` to `Q3 Report Résumé (final) — v2!.docx` (spaces, an accented unicode character, parentheses, an em-dash, and an exclamation mark). | Rename succeeds; the full new name displays correctly with no mangled characters, truncation, or encoding artifacts. |
| 4 | Refresh the page/bucket view. | All renamed names persist correctly after reload (confirms server-side storage, not just client-side rendering). |
| 5 | From the table, download `Alpha-Renamed.docx`. | Download succeeds using the new filename with correct content. |
| 6 | Open a preview of `Alpha-Renamed.docx`. | Preview opens correctly under the new name. |
| 7 | Delete `Alpha-Renamed.docx`. | Deletion succeeds; file no longer appears in the table. |

## Expected Final State

Both rename entry points produce a fully consistent, refreshed table state; filenames containing spaces, unicode characters, and symbols are supported end-to-end; the renamed file remains fully functional (downloadable, previewable, deletable) until intentionally removed.

## Pass/Fail Criteria

**Pass:** All 7 steps succeed exactly as described, including the automatic preview close in step 2 and correct persistence after reload in step 4.
**Fail:** The table fails to refresh, the old name persists, the preview stays open after renaming from within it, any character is mangled/truncated, or any post-rename action (download/preview/delete) fails.
