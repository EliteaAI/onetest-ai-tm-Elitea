---
id: ELITEA-0353
title: "Chat attachment upload of file >200k chars returns size-limit error — 200k limit intentionally preserved"
priority: high
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0353: Chat attachment upload of file >200k chars returns size-limit error — 200k limit intentionally preserved

**Module:** Artifacts Toolkit Read File · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a file exceeding 200k chars is uploaded as a Chat attachment and then read via the attachment processing path (elitea_core), the size-limit error is returned — this limit is intentionally preserved for Chat to prevent LLM context flooding.

**Coverage:**
- elitea_core hardcodes `skip_size_check=False` for chat attachment reads
- File >200k chars attached to Chat triggers size-limit error on the read path
- This is expected and correct behavior — not a bug

## Preconditions

- Logged in to {{base_url}}
- Chat with file attachment capability enabled (paperclip icon visible)
- Local file `xlarge_file.txt` (~300k chars) prepared for attachment
- Chrome or Edge, latest stable

## Test Data

- File to attach: `xlarge_file.txt` (~300,000 chars, exceeds 200k limit)
- Chat message: `"Summarize the attached file"`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar. Start a new direct LLM conversation. | Chat interface opens with paperclip icon visible. |
| 2 | Click the paperclip icon. Attach `xlarge_file.txt` (~300k chars). Send message: "Summarize the attached file" | File uploaded. Message sent. |
| 3 | Inspect the chat response. | Response contains a size-limit error indication — the file was too large to be processed via the chat attachment path. LLM does not receive full 300k content. |

## Expected Final State

Response contains a size-limit error indication — the file was too large to be processed via the chat attachment path. LLM does not receive full 300k content.

## Pass/Fail Criteria

**Pass:**
- Size-limit error returned for >200k file on chat attachment path
- This is correct expected behavior (intentional constraint)

**Fail:**
- Full 300k content silently fed to the LLM (limit not enforced, context flooding risk)
- Generic error unrelated to file size
