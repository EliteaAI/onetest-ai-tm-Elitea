---
id: ELITEA-2585
title: "Trace steps endpoint filters by kind (tool_call vs thinking_step)"
priority: medium
type: functional
module: trace-steps-api
status: ready
execution_type: manual
tags: [nfr:performance, eng:backend, epic:5724]
requirements: [EliteaAI/elitea_issues#5724, EliteaAI/elitea_issues#5727]
---
# ELITEA-2585: Trace steps endpoint filters by kind (tool_call vs thinking_step)

**Module:** Trace Steps API · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the trace steps endpoint supports filtering by `kind` parameter to return only tool_calls or only thinking_steps.

**Coverage:**
- Filter by kind=tool_call returns only tool calls
- Filter by kind=thinking_step returns only thinking steps
- No filter returns both types

## Preconditions

- Logged in to {{base_url}}
- Access to a conversation that has both tool_calls AND thinking_steps
- API testing tool available (Postman, curl, or DevTools)

## Test Data

| Field | Value |
|-------|-------|
| Endpoint | `GET /api/v2/elitea_core/message_traces/{workspace}/{project}/{conversation_id}` |
| Query param | `kind=tool_call` or `kind=thinking_step` |
| Conversation | One with both tool calls and thinking steps |
| Model | Anthropic model with extended thinking enabled (e.g., GPT-5.2) |
| Agent | Agent with tools configured (e.g., GitHub toolkit) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create conversation using model with extended thinking + tools (or use existing) | Conversation has both thinking_steps and tool_calls |
| 2 | Call `/message_traces/...` endpoint WITHOUT kind parameter | Returns all items (note the total count, e.g., 3 items: 2 tool_calls + 1 thinking_step) |
| 3 | Call same endpoint with `&kind=tool_call` added to URL | Returns ONLY items with `"kind": "tool_call"` (count should be less than step 2) |
| 4 | Verify all returned items in step 3 have `"kind": "tool_call"` | No `"kind": "thinking_step"` items in response |
| 5 | Call same endpoint with `&kind=thinking_step` | Returns ONLY items with `"kind": "thinking_step"` |
| 6 | Verify all returned items in step 5 have `"kind": "thinking_step"` | No `"kind": "tool_call"` items in response |
| 7 | Verify counts: (step 3 count) + (step 5 count) = (step 2 count) | No items lost or duplicated across filters |
| 8 | Call with invalid kind value `&kind=invalid_value` | Returns error 400 or empty result (document actual behavior) |

## Expected Final State

Filtering by `kind` parameter correctly separates tool_calls from thinking_steps. The sum of filtered results equals the unfiltered total. Example:
- No filter: 3 items total
- `kind=tool_call`: 2 items
- `kind=thinking_step`: 1 item
- 2 + 1 = 3 ✅

## Pass/Fail Criteria

**Pass:**
- kind=tool_call returns only tool calls
- kind=thinking_step returns only thinking steps
- No filter returns both
- Invalid kind handled gracefully

**Fail:**
- Wrong items returned for a filter
- Mixed results when filter is applied
- Server error on invalid kind
