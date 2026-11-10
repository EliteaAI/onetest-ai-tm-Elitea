---
id: ELITEA-4463
title: "Import rejects wrong-type, mismatched-feature, and tampered files with the exact specified error text"
priority: critical
type: security
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-import, security, issue:6904, p0]
requirements: ["EliteaAI/elitea_issues#6904"]
---

# ELITEA-4463: Import rejects wrong-type, mismatched-feature, and tampered files with the exact specified error text

**Module:** chat-interface · **Priority:** Critical · **Type:** Security

**Objective:** Verify Import's file-type and integrity validation produces the exact specified error text, and never accepts a wrong-type, mismatched-feature, or tampered file.

---

## Preconditions

- A file produced by a different export feature that happens to use the same encrypted-file extension as chat exports (e.g. a project/environment backup export, if this platform has one) — used to confirm the content check is specific to chat exports, not just "any file with this extension."
- Any file with a non-matching extension (e.g. a plain `.txt` file).
- A valid chat export file (from any chat), with a copy of it that has had a few bytes changed mid-file (extension left untouched).

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Import file picker, browse to a folder containing the non-matching-extension file. | That file is not visible/selectable in the picker at all — filtered out at the OS dialog level. |
| 2 | Select and attempt to import the different-feature's export file (same extension, wrong content type). | Rejected with exactly: "Invalid file: only encrypted chat files exported from ELITEA can be imported." Import stays disabled; nothing created. |
| 3 | Attempt to import the tampered copy of the valid chat export. | Rejected with exactly: "Invalid file: the file is corrupted or has been modified." Nothing imported. |

## Expected Final State

Only genuine, unmodified chat-export files ever import successfully; every mismatch produces the exact specified error.

## Pass/Fail Criteria

**Pass:**
- Both error messages match exactly; the picker filters the non-matching-extension file.

**Fail:**
- Any wrong-type/tampered file accepted, or a generic error instead of the specific text.
