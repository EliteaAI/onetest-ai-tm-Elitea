---
id: ELITEA-0492
title: "Verify Programming File Accepted in Chat Conversation - Core File Types"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [programming-files, feat:attachments, story:3671, r-2.0.1, smoke, chat]
requirements: [ProjectAlita/projectalita.github.io#3671]
---
# ELITEA-0492: Verify Programming File Accepted in Chat Conversation - Core File Types

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the core programming file types (.py, .js, .ts, .java) are accepted by the chat attachment button after the backend returns them in the `code_types` API response. These are the most commonly used languages and represent the primary user value of this feature.

## Preconditions

1. User is logged into Elitea platform with a valid account
2. A Chat conversation exists (LLM/direct chat, not agent-based)
3. The backend API for the project returns `.py`, `.js`, `.ts`, `.java` in the `code_types` field of `/index_types/prompt_lib/{projectId}`
4. Sample code files are available: `app.py`, `index.js`, `types.ts`, `Main.java`

## Test Data

- `app.py`: A Python file containing a simple class definition (~1KB)
- `index.js`: A JavaScript file with a function (~500 bytes)
- `types.ts`: A TypeScript interface file (~500 bytes)
- `Main.java`: A Java class file (~1KB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation | The conversation is displayed with the message input area and the attachment (paperclip) button visible |
| 2 | Click the attachment button | The native OS file picker dialog opens |
| 3 | In the file picker, verify that `.py` files are listed as accepted types in the filter | The file picker's accepted type filter includes `.py` files (and other code file types) |
| 4 | Select `app.py` and confirm | The file picker closes; `app.py` appears in the attachment list below the message input. No error toast is displayed. |
| 5 | Click the attachment button again and select `index.js` | `index.js` is added to the attachment list. Total attachments now show 2. |
| 6 | Click the attachment button again and select `types.ts` | `types.ts` is added to the attachment list. Total count shows 3. |
| 7 | Click the attachment button again and select `Main.java` | `Main.java` is added to the attachment list. Total count shows 4. |
| 8 | Verify that each attachment shows a filename label and file size | All 4 attachments display their respective filenames and sizes in KB |

## Expected Final State

All 4 attachments display their respective filenames and sizes in KB

## Pass/Fail Criteria

PASS: All 4 files attach without error toasts; each file appears in the attachment list with the correct filename; the total count reflects all 4 files
FAIL: Any file triggers "Invalid file types detected" error toast; any file is silently rejected; the file picker does not list code files as accepted; any error message references an unsupported file type
