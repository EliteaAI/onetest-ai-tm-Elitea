---
id: ELITEA-2583
title: "GET Conversation Details does not return tool_calls/thinking_steps in meta for new conversations"
priority: critical
type: functional
module: trace-steps-api
status: ready
execution_type: manual
tags: [nfr:performance, eng:backend, epic:5724]
requirements: [EliteaAI/elitea_issues#5724, EliteaAI/elitea_issues#5727]
---
# ELITEA-2583: GET Conversation Details does not return tool_calls/thinking_steps in meta for new conversations

**Module:** Trace Steps API · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that GET conversation details API endpoint no longer returns `tool_calls` and `thinking_steps` in `message_group.meta` for conversations created after the migration. This is critical for performance — the heavy keys are now stored in a separate table.

**Coverage:**
- New conversations do NOT have tool_calls in message_group.meta
- New conversations do NOT have thinking_steps in message_group.meta
- Response size is significantly smaller than before

## Preconditions

- Logged in to {{base_url}}
- Access to an agent with tool calling capabilities
- Browser DevTools → Network tab open and recording
- Migration to message_trace_step table is deployed

## Test Data

| Field | Value |
|-------|-------|
| Endpoint | `GET /api/v2/elitea_core/conversation/{workspace}/{project}/{conversation_id}` |
| Agent | Any agent with tools configured |
| Tool | Any tool that will be invoked |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new conversation with an agent that has tools | Conversation is created successfully |
| 2 | Send a message that triggers tool execution | Agent responds using tools, tool calls are visible in UI |
| 3 | Open DevTools Network tab and filter by XHR/Fetch | Network requests are visible |
| 4 | Refresh the page or navigate to the conversation to trigger GET conversation details | GET request to `/api/v2/elitea_core/conversation/{workspace}/{project}/{conversation_id}` is captured |
| 5 | Inspect the response JSON, navigate to `message_groups[].meta` | message_group objects are visible in response |
| 6 | Check if `meta.tool_calls` exists in any message_group | `meta.tool_calls` key is **NOT present** |
| 7 | Check if `meta.thinking_steps` exists in any message_group | `meta.thinking_steps` key is **NOT present** |
| 8 | Verify tool calls are still visible in the UI | Tool call pins are displayed correctly (loaded from `/message_traces/` endpoint) |
| 9 | Note the response size in Network tab | Response size is noticeably smaller than before migration |

## Expected Final State

The GET conversation details response (`/api/v2/elitea_core/conversation/...`) does not contain `tool_calls` or `thinking_steps` keys in `message_groups[].meta`. The UI still displays tool calls correctly, loaded from the separate `/api/v2/elitea_core/message_traces/...` endpoint.

## Pass/Fail Criteria

**Pass:**
- `meta.tool_calls` is absent or empty in all message_groups
- `meta.thinking_steps` is absent or empty in all message_groups
- Tool calls are still visible in UI (loaded from new endpoint)

**Fail:**
- `meta.tool_calls` or `meta.thinking_steps` still present with data
- Tool calls not visible in UI
