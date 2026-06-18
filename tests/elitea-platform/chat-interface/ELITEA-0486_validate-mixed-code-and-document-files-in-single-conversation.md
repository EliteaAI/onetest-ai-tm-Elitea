---
id: ELITEA-0486
title: "Validate Mixed Code and Document Files in Single Conversation"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [programming-files, feat:attachments, mixed-types, story:3671, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3671]
---
# ELITEA-0486: Validate Mixed Code and Document Files in Single Conversation

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that code files and non-code files (documents, images) can coexist in the same attachment list in a single conversation, and that the AI can process both types in the same message. This tests the realistic use case where a developer attaches code alongside supporting documentation.

## Preconditions

1. User is logged into Elitea platform
2. A Chat conversation is open with a capable LLM
3. Backend returns both `code_types` (including `.py`) and `document_types` (including `.txt`) for the project
4. Test files available: `implementation.py` and `requirements.txt`

## Test Data

- `implementation.py`: Python code file implementing a simple feature (~1KB)
- `requirements.txt`: A plain text requirements document describing what the code should do (~200 bytes)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation | Conversation is displayed |
| 2 | Click attachment button and select `implementation.py` | Python file attaches. Count: 1. |
| 3 | Click attachment button and select `requirements.txt` | Text file attaches. Count: 2. Both files visible in attachment list. |
| 4 | Type: "Based on the requirements in requirements.txt, does implementation.py correctly implement all the requirements?" | Text appears in input |
| 5 | Send the message | Both files and message are sent; AI processes |
| 6 | Verify the AI response references both files (mentions requirements from the .txt file and checks them against the .py code) | AI response demonstrates cross-referencing of both attachments |

## Expected Final State

AI response demonstrates cross-referencing of both attachments

## Pass/Fail Criteria

- PASS: Both file types attach without errors; attachment list shows both files; AI response references content from both files; no type conflict errors
- FAIL: Second file type is rejected due to a type conflict; attachment list shows only one file type; AI cannot access one of the files; any error during send
