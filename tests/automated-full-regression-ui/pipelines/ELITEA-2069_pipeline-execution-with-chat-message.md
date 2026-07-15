---
id: ELITEA-2069
title: "Pipeline — Execution with Chat Message"
priority: high
type: functional
module: pipelines
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-2069: Pipeline — Execution with Chat Message

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that a pipeline with a working LLM → Printer → END configuration can be executed by sending a chat message, and that a response is returned with a streaming indicator.

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline with a working LLM → Printer → END configuration exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline with a working LLM → Printer → END configuration | Pipeline is loaded with chat panel visible |
| 2 | In the chat panel, type a message in "Type your message..." textbox | Message is entered in the chat input |
| 3 | Press Enter or click Send | Message is submitted |
| 4 | Verify a loading/streaming indicator appears | Streaming/loading indicator is visible during processing |
| 5 | Verify response message appears in the chat area | Response from the pipeline is displayed |
| 6 | Verify the chat starter (if configured) is clickable and sends the message | Chat starter button is functional |

---

## Expected Final State

The pipeline processes the chat message, shows a streaming indicator during execution, and returns a response in the chat panel. Chat starters (if configured) are clickable and functional.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Message is sent, streaming indicator appears, and response is received in the chat.

**Fail:**
- Any step produces an error or unexpected result.
- Message is not sent, no streaming indicator, or no response appears.
