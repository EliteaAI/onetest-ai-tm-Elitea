---
id: ELITEA-0488
title: "Verify Code File Rejected When Extension Not in Backend Code Types"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [programming-files, feat:attachments, negative-testing, story:3671, validation, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3671]
---
# ELITEA-0488: Verify Code File Rejected When Extension Not in Backend Code Types

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that a file with an extension NOT present in the backend's `code_types` (or any other allowed type list) is correctly rejected with an appropriate error message. The validation must work correctly to prevent unauthorized file types.

## Preconditions

1. User is logged into Elitea platform
2. A Chat conversation is open
3. The backend API returns a `code_types` that includes common extensions but explicitly does NOT include `.abc` or `.unknown`
4. A test file `script.abc` exists with plain text content (renamed to have an unsupported extension)

## Test Data

- `script.abc`: A text file renamed with an unsupported extension (.abc is not a real programming language)
- `real_code.py`: A valid Python file available for comparison

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation | Conversation is displayed |
| 2 | Click the attachment button | File picker opens |
| 3 | Select `script.abc` | File picker closes; an error toast appears indicating the file type is invalid (e.g., "Invalid file types detected: .abc") |
| 4 | Verify that `script.abc` does NOT appear in the attachment list | The attachment list remains empty (or unchanged from before) |
| 5 | Click attachment button again and select `real_code.py` | `real_code.py` is accepted and appears in the attachment list — confirming the valid file still works after the rejection |

## Expected Final State

`real_code.py` is accepted and appears in the attachment list — confirming the valid file still works after the rejection

## Pass/Fail Criteria

- PASS: `script.abc` triggers an error toast with the invalid extension mentioned; file does NOT appear in attachment list; subsequent valid `.py` file is accepted normally
- FAIL: `script.abc` is accepted without error; no error message shown; valid `.py` file is rejected after the invalid file attempt; platform crashes or enters an error state
