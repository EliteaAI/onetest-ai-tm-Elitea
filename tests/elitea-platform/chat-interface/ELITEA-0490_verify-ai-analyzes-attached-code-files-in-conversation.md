---
id: ELITEA-0490
title: "Verify AI Analyzes Attached Code Files in Conversation"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [programming-files, feat:attachments, ai-analysis, story:3671, r-2.0.1, smoke, chat]
requirements: [ProjectAlita/projectalita.github.io#3671]
---
# ELITEA-0490: Verify AI Analyzes Attached Code Files in Conversation

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the core user story: after attaching a Python code file to a conversation and sending a message asking the AI to analyze it, the AI correctly reads and analyzes the code content. This is the primary end-to-end validation of the feature.

## Preconditions

1. User is logged into Elitea platform
2. A Chat conversation is open with a capable LLM (e.g., GPT-4o, Claude Sonnet, or similar multimodal/text model)
3. Backend returns `.py` in `code_types` for the project
4. A Python file `buggy_sort.py` is available with the following content:

def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n-i-2):  # Bug: should be n-i-1
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
    return arr

## Test Data

- File: `buggy_sort.py` (approximately 200 bytes, contains a bubble sort Python function with an intentional off-by-one bug: loop range uses `n-i-2` instead of `n-i-1`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation with an LLM participant | Conversation is displayed |
| 2 | Click the attachment button and select `buggy_sort.py` | `buggy_sort.py` appears in the attachment list. No error toast. |
| 3 | In the message input, type: "Please review this Python code and identify any bugs" | Text appears in the input field |
| 4 | Send the message (click Send or press Enter) | Message and attachment are sent; AI begins processing |
| 5 | Wait for the AI response | AI responds with a code review |
| 6 | Verify the AI response references content from the Python file | The AI response mentions the `bubble_sort` function, identifies the off-by-one bug in the range (`n-i-2` should be `n-i-1`), or otherwise demonstrates it has read the file content |

## Expected Final State

The AI response mentions the `bubble_sort` function, identifies the off-by-one bug in the range (`n-i-2` should be `n-i-1`), or otherwise demonstrates it has read the file content

## Pass/Fail Criteria

- PASS: AI response demonstrates awareness of the file content (mentions function name, identifies the bug, or references specific code elements); no error during send or processing
- FAIL: AI claims it cannot read the attachment; AI response is generic with no reference to the file content; error toast appears during or after sending; the message fails to send
FAIL: AI receives an empty or garbled file content
