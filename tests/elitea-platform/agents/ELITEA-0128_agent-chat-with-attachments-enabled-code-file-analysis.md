---
id: ELITEA-0128
title: "Agent Chat with Attachments Enabled - Code File Analysis"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [programming-files, feat:attachments, story:3671, r-2.0.1, agent]
requirements: [ProjectAlita/projectalita.github.io#3671]
---
# ELITEA-0128: Agent Chat with Attachments Enabled - Code File Analysis

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a programming file can be attached and analyzed in a conversation where an Agent (with attachments enabled) is a participant. Agents require `attachments` to be included in their `internal_tools` list for the attachment button to be active.

## Preconditions

1. User is logged into Elitea platform with Editor or Admin permissions on the project
2. An Agent exists with "Allow attachments" toggle enabled in its configuration (the `attachments` internal tool is included)
3. A Chat conversation exists with this Agent as a participant
4. Backend returns `.py` in `code_types` for the project
5. A Python file `analysis_target.py` (~1KB, ~50 lines of Python code) is available

## Test Data

- Agent: Any agent with attachments enabled and a suitable LLM (e.g., GPT-4o or Claude Sonnet)
- File: `analysis_target.py` containing a moderately complex Python class with methods

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation with the Agent as a participant | Conversation opens; the attachment button is visible and enabled (not grayed out) |
| 2 | Verify the attachment button tooltip shows remaining capacity (e.g., "10 attachments remaining") | Tooltip confirms attachments are available |
| 3 | Click the attachment button and select `analysis_target.py` | `analysis_target.py` appears in the attachment list. No error toast. |
| 4 | Type: "Summarize what this Python code does and suggest improvements" | Text appears in input |
| 5 | Send the message | Message and attachment are sent; Agent begins processing |
| 6 | Wait for Agent response | Agent responds |
| 7 | Verify the Agent's response references the Python code content (e.g., mentions class/function names, describes logic, or suggests specific improvements based on the code) | Response demonstrates the Agent read the file content |

## Expected Final State

Response demonstrates the Agent read the file content

## Pass/Fail Criteria

- PASS: Attachment button is enabled for the Agent conversation; file attaches without error; Agent response references actual content from the file
- FAIL: Attachment button is disabled for the Agent conversation despite attachments being enabled; file is rejected; Agent responds without referencing the code content; any error during execution
