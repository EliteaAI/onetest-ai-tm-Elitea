---
id: ELITEA-4540
title: "Verify extracted content and search snippets are truncated/capped and presented as external, untrusted content"
priority: high
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit attached to an agent, with a known Max Page Chars value (e.g. lowered to 500 for easier testing)

## Test Data

| Field | Value |
|-------|-------|
| Max Page Chars | 500 |
| Long page | A public page exceeding 500 characters |
| Broad query | A topic returning multiple search snippets |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Lower Max Page Chars to 500 on the toolkit | Setting saved |
| 2 | Ask the agent to extract the long page | Content is cut off at approximately 500 characters with a truncation indicator/marker, not silently cut |
| 3 | Ask the agent to search the broad topic and inspect returned snippets | Each snippet is reasonably short (not full-page-length) |
| 4 | Inspect the tool output area in the chat/agent transcript | Content is visually distinguished as external/fetched data (e.g. a tool-call card), not presented as the model's own untagged text |

## Expected Final State

Extracted content and snippets are confirmed to be capped and visually marked as external content.

## Pass/Fail Criteria

**Pass:**
- Truncation marker is present for over-limit content
- Snippets stay short
- Tool output is visually distinguished as external

**Fail:**
- Content is truncated with no marker
- Snippets are excessively long
- Tool output is indistinguishable from the model's own text
