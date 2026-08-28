---
id: ELITEA-2939
title: "Pipeline with mixed LLM, Toolkit, and MCP nodes added to a chat completes end-to-end after resolving both auth-requiring nodes"
priority: high
type: integration
module: toolkit-authorization
status: draft
execution_type: manual
tags: [feat:mcp-remote, feat:toolkits, int:openapi, int:sharepoint, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6072]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A pipeline contains a mix of node types: an LLM node, a Toolkit node (delegated toolkit, no valid token), and an MCP node (OAuth-requiring Remote MCP, no active session)
- The pipeline is added as a participant in a chat conversation

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline structure | LLM node → Toolkit node (auth required) → MCP node (auth required) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In the chat, send a message that triggers the pipeline | Pipeline run starts; LLM node executes normally |
| 2 | Observe the run reaching the Toolkit node | "Toolkit Authorization Required" popup appears for the Toolkit node |
| 3 | Authorize the Toolkit node's popup | Toolkit node executes; run advances to the MCP node |
| 4 | Observe the run reaching the MCP node | "Toolkit Authorization Required" popup appears for the MCP node |
| 5 | Authorize the MCP node's popup | MCP node executes |
| 6 | Observe overall pipeline completion in the chat | Pipeline completes end-to-end and a final result is streamed into the chat |

## Expected Final State

A mixed-node pipeline (LLM + Toolkit + MCP) running as a chat participant correctly pauses at each auth-requiring node in turn and completes end-to-end once both are resolved via Authorize.

## Pass/Fail Criteria

**Pass:**
- Both the Toolkit node and MCP node correctly pause with their own popups, in pipeline order
- Pipeline completes end-to-end in the chat after both are authorized, with a final result streamed

**Fail:**
- Either auth-requiring node fails to pause/surface a popup
- Pipeline does not complete or does not stream a final result to the chat after both authorizations
