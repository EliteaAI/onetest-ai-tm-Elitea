---
id: ELITEA-3323
title: "Unsaved changes warning appears when closing Agent comparison modal with pending edits"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Agent exists with 2+ versions

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Original Instructions | "Original text before edit" |
| Edited Instructions | "Modified text that is not saved" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for Test Agent | Modal opens successfully |
| 2 | Edit Instructions text in Version 1 to "Modified text that is not saved" (do NOT click Save) | Text updates in the field, unsaved state |
| 3 | Attempt to close modal by clicking X button | Confirmation dialog appears |
| 4 | Verify dialog message reads: "You have unsaved changes in the compared versions. Closing this comparison will discard them." | Correct warning message displayed |
| 5 | Verify dialog has two action buttons: "Stay" (or "Cancel") and "Discard" (or "Close") | Both buttons are present |
| 6 | Click "Stay" or "Cancel" button | Dialog closes, comparison modal remains open |
| 7 | Verify edited text is still present in Version 1 Instructions field | Text shows "Modified text that is not saved" (edit preserved) |
| 8 | Attempt to close modal again via X button | Confirmation dialog appears again |
| 9 | Click "Discard" or "Close" button | Comparison modal closes, returns to Agent details page |
| 10 | Reopen Compare Versions modal | Modal opens with fresh data |
| 11 | Verify Version 1 Instructions shows original text (changes were NOT saved) | Field displays "Original text before edit" |
| 12 | Edit multiple fields: Instructions, Welcome Message, and Chat Starter (do not save any) | All fields updated but unsaved |
| 13 | Attempt to close modal | Warning dialog appears (multiple unsaved changes) |
| 14 | Click "Discard" | Modal closes |
| 15 | Open modal with no edits made | Modal opens |
| 16 | Immediately click X button to close (no edits) | Modal closes without warning dialog (no unsaved changes) |

## Expected Final State

Unsaved changes warning displays when closing modal with pending edits, allows user to stay or discard, and does not appear when no changes were made.

## Pass/Fail Criteria

**Pass:**
- Warning dialog appears when closing with unsaved edits
- Correct warning message displayed
- "Stay" preserves edits and keeps modal open
- "Discard" closes modal and loses unsaved changes
- No warning when no edits were made

**Fail:**
- No warning dialog when unsaved changes exist
- Incorrect warning message
- "Stay" closes modal or loses edits
- Warning appears when no changes were made
