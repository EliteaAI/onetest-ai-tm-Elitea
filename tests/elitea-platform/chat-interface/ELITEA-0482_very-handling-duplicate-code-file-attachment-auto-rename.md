---
id: ELITEA-0482
title: "Very Handling Duplicate Code File Attachment - Auto-Rename"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [duplicate-handling, programming-files, feat:attachments, story:3671, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3671]
---
# ELITEA-0482: Very Handling Duplicate Code File Attachment - Auto-Rename

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that attaching the same code file twice (same filename) causes the second file to be auto-renamed with a timestamp-based appendix rather than silently dropped or overwriting the first. The `validateAttachmentFiles` function has duplicate detection and auto-rename logic that generates a name like `filename_20251106_143022_1.50KB.ts`.

## Preconditions

1. User is logged into Elitea platform
2. A Chat conversation is open
3. Backend returns `.ts` in `code_types` for the project
4. A TypeScript file `service.ts` (~1KB) is available — needs to be selectable twice

## Test Data

- `service.ts`: A TypeScript service file (~1KB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation | Conversation is displayed |
| 2 | Click attachment button and select `service.ts` | `service.ts` appears in the attachment list with the original name. Count: 1. |
| 3 | Click attachment button again and select `service.ts` a second time | Second file processes; attachment list now shows 2 entries |
| 4 | Verify the second attachment in the list has a different name from the first (the name contains a timestamp appendix, e.g., `service_20260305_143022_1.00KB.ts`) | The second attachment shows a modified filename with timestamp/size appendix. The first attachment retains its original name `service.ts`. |
| 5 | Verify no error toast is shown for the duplicate | The duplicate is handled silently via auto-rename; no error message about duplicates |

## Expected Final State

The duplicate is handled silently via auto-rename; no error message about duplicates

## Pass/Fail Criteria

- PASS: Two entries appear in the attachment list; second entry has a modified name with timestamp/size appendix; no error toast about duplicates; first entry retains original name
- FAIL: Second file is silently dropped (only 1 entry in list); second file overwrites or merges with first; an error toast incorrectly blocks the duplicate from being added; the rename appendix format is missing the timestamp or extension
