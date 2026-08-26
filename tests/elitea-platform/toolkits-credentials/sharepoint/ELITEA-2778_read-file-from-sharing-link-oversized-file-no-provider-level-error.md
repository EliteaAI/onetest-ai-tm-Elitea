---
id: ELITEA-2778
title: "Oversized File via read_file_from_sharing_link No Longer Produces a Provider-Level Error"
priority: critical
type: regression
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:toolkits, issue:6051, oversized-file, content-too-large, read_file_from_sharing_link]
requirements: [EliteaAI/elitea_issues#6051]
---
# ELITEA-2778: Oversized File via read_file_from_sharing_link No Longer Produces a Provider-Level Error

**Module:** Sharepoint · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that invoking `read_file_from_sharing_link` on a file whose parsed content exceeds the provider's message-length limit (while still under the 20MB download-size cap) no longer raises a provider/LLM-level error such as Azure `BadRequestError: string too long`, and instead returns a structured, self-describing response indicating the content was too large to return in full.

## Preconditions

- SharePoint Delegated credential is connected and authenticated
- A text file sized to reproduce the original failure (~11MB / ~12,043,364 parsed characters) exists and is shared via a sharing link
- Agent/chat is configured with the SharePoint toolkit and has access to `read_file_from_sharing_link`

## Test Data

| Field | Value |
|-------|-------|
| File size (download) | ~11MB |
| Parsed character count | ~12,043,364 characters |
| Sharing method | Sharing link |
| Reference | Original failure: Azure/LLM `BadRequestError: string too long` (Issue #6051) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Via chat/agent, invoke `read_file_from_sharing_link` with the sharing link of the oversized file | Call completes without raising a provider/LLM error; no `BadRequestError`, no "string too long" message, and no equivalent unhandled exception |
| 2 | Inspect the returned response | Response is a structured, well-formed object explicitly indicating the content was too large to return in full — not a crash, not silent truncation, and not a raw partial dump of file content |
| 3 | Inspect the "too large" indication within the response | It reflects the file's true size/length in some form (a size/length indicator is present and its value is greater than whatever cap the tool reports); do not assert the exact `200000` constant — only that the reported length exceeds the reported cap |

## Expected Final State

The tool call completes successfully end-to-end (no provider exception propagates to the agent/chat). The final response the user sees is a structured "content too large" object whose length/size indicator is greater than the tool's reported cap, correctly reflecting that the oversized file was capped rather than silently truncated or having crashed the call.

## Pass/Fail Criteria

**Pass:**
- No provider/LLM exception (`BadRequestError`/"string too long"/equivalent) is raised at any point
- A structured, self-describing "too large" response is returned
- The response's size/length indicator is present and is greater than the cap value the tool reports

**Fail:**
- A provider/LLM exception is raised (crash propagates to agent/chat)
- Or the response is a silent truncated/garbled dump of content with no indication that it was capped
