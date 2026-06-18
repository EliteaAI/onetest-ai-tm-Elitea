---
id: ELITEA-0356
title: "Chat attachment upload of file ≤200k chars works correctly — no regression"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0356: Chat attachment upload of file ≤200k chars works correctly — no regression

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that attaching a file within the 200k limit via Chat still works correctly after the elitea_core change — no regression on the within-limit happy path.

**Coverage:**
- File ≤200k attached and processed normally in Chat
- LLM receives file content and responds meaningfully
- `skip_size_check=False` on chat path does not affect files within the limit

## Preconditions

- Logged in to {{base_url}}
- Chat with file attachment capability enabled (paperclip icon visible)
- Local file `medium_file.txt` (~80k chars) prepared for attachment
- Chrome or Edge, latest stable

## Test Data

- File to attach: `medium_file.txt` (~80,000 chars, within 200k limit)
- Chat message: `"Summarize the attached file"`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Start a new direct LLM conversation. | Chat interface opens with paperclip icon visible. |
| 2 | Click the paperclip icon. Attach `medium_file.txt` (~80k chars). Send message: "Summarize the attached file" | File attached and message sent successfully. |
| 3 | Inspect the chat response. | LLM returns a meaningful summary based on the file content. No size-limit error. File processed correctly. |

## Expected Final State

LLM returns a meaningful summary based on the file content. No size-limit error. File processed correctly.

## Pass/Fail Criteria

**Pass:**
- File within 200k limit processed correctly via Chat attachment path
- LLM responds with content-based summary
- No size-limit error

**Fail:**
- Size-limit error for a file within the 200k limit (regression)
- Response empty or unrelated to file content
