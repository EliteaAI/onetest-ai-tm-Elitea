---
id: ELITEA-3240
title: "Large Project Context (~10K Characters) Handles Correctly"
priority: critical
type: functional
module: project-context
status: draft
execution_type: manual
tags: [project-context, chat, agents, r-2.0.6, eng:optimization, edge-case]
requirements: [EliteaAI/elitea_issues#5326]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Large Project Context prepared (~10,000 characters of content)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Project Context Size | ~10,000 characters (approaching system limit) |
| Test Query | `"Summarize the key points from the project context"` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set Project Context to large content (~10K characters) | Context saved successfully |
| 2 | Start new chat, ask: "Summarize the key points from the project context" | Chat invokes `read_project_context` tool, processes and responds with summary |
| 3 | Verify response contains information from large context | Context correctly injected and used |
| 4 | Run agent with same query | Agent also invokes `read_project_context` tool, handles large context correctly |
| 5 | Verify no errors or warnings in UI/console | No errors related to large context size |

## Expected Final State

Large Project Context (~10K characters) handled correctly. No errors, degradation, or failures. Tool call visible in both chat and agent.

## Pass/Fail Criteria

**Pass:**
- Large context saved and applied successfully
- Chat and agent handle large context without errors
- Responses contain context information
- `read_project_context` tool call visible in UI
- No performance degradation or errors

**Fail:**
- Large context causes errors or failures
- Context truncated or lost
- Tool call not visible
- Significant performance degradation
- Errors in logs or UI
