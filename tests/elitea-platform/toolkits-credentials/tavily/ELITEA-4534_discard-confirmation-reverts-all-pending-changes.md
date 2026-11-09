---
id: ELITEA-4534
title: "Verify the Discard confirmation dialog reverts all pending changes on the Configuration page"
priority: high
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit open in edit mode

## Test Data

| Field | Edited value |
|-------|--------------|
| Toolkit Name | A new name |
| Max Results | A different value |
| Credential | A different credential |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Edit Toolkit Name, Max Results, and the selected credential without saving | All three pending edits are present |
| 2 | Click "Discard" | A confirmation dialog appears |
| 3 | Click "Cancel" in the dialog | All pending edits are still present |
| 4 | Click "Discard" again and confirm it | Every edited field reverts to its last-saved value, not just some of them |
| 5 | Observe "Save" and "Discard" button state immediately after a successful discard | Both become disabled again (no pending changes remain) |

## Expected Final State

Discard is confirmed to fully revert every pending field, not a partial subset.

## Pass/Fail Criteria

**Pass:**
- All edited fields revert together after confirming Discard
- Save/Discard disable afterward

**Fail:**
- Any edited field fails to revert
- Save/Discard remain enabled after a successful discard
