---
id: ELITEA-2589
title: "UI displays thinking steps correctly from new paginated source"
priority: high
type: functional
module: trace-steps-api
status: ready
execution_type: manual
tags: [eng:frontend, epic:5724]
requirements: [EliteaAI/elitea_issues#5724, EliteaAI/elitea_issues#5728]
---
# ELITEA-2589: UI displays thinking steps correctly from new paginated source

**Module:** Trace Steps API · **Priority:** High · **Type:** Functional

**Objective:** Verify that the UI correctly renders thinking steps from the new paginated trace steps endpoint for new conversations.

**Coverage:**
- Thinking steps are displayed in the conversation
- Thinking content is visible
- Empty thinking steps are filtered (not shown)
- Model name is displayed (if applicable)

## Preconditions

- Logged in to {{base_url}}
- Access to an agent using Anthropic model with extended thinking enabled
- Migration to message_trace_step is deployed

## Test Data

| Field | Value |
|-------|-------|
| Model | Claude 4.5 Sonnet or higher (Anthropic models show thinking by default) |
| Agent | Any agent configured to use Claude Sonnet/Opus |
| Complex prompt | "Analyze the pros and cons of migrating a monolithic architecture to microservices for a 10-year-old legacy system with 5M+ users. Consider technical debt, team structure, and risk mitigation." |
| Simple prompt (for comparison) | "What is 2+2?" (will still show thinking for Claude models) |
| Prompt | Analyze the pros and cons of migrating a monolithic architecture 
to microservices for a 10-year-old legacy system with 5M+ users. 
Consider technical debt, team structure, and risk mitigation |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create conversation with Claude 4.5 Sonnet agent | Conversation is created |
| 2 | Send complex message (e.g., microservices migration analysis) | Agent thinks and responds |
| 3 | Observe the thinking section in response | Thinking section visible: "Thought for X secs" with collapse/expand |
| 4 | Verify model name badge is shown | "Anthropic Claude 4.5 Sonnet" badge visible |
| 5 | Click on thinking section (model badge or arrow) to expand | Modal/panel opens showing full thinking text with "**🧠 Thinking:**" header |
| 6 | Verify thinking content is readable and formatted | Text is complete, markdown formatted, no truncation |
| 7 | Call `/message_traces/` API for this conversation | Returns thinking_steps with `"kind": "thinking_step"` |
| 8 | Check if any thinking_step has empty text (`"text": ""` or `"thinking": null`) in API | Document result: if empty steps exist, proceed to step 9 |
| 9 | If empty steps found in API, verify UI does NOT show them | Empty thinking_steps are filtered out and not visible in UI |
| 10 | Compare thinking_step count in API vs UI visible count | Counts match (UI count = API count - empty steps) |

## Expected Final State

Thinking section is visible with collapse/expand functionality. Full thinking text is displayed in a modal when expanded, with model name badge shown. Technically empty thinking steps (where `text=""` or `thinking=null` in API) are filtered out and not displayed in UI.

**Note:** Claude 4.5 Sonnet shows thinking for ALL queries, even simple ones like "What is 2+2?". This is expected behavior — the "empty steps" check refers to technically empty text fields in the API response, not absence of thinking for simple queries.

## Pass/Fail Criteria

**Pass:**
- Thinking section visible with "Thought for X secs" label
- Model name badge displayed ("Anthropic Claude 4.5 Sonnet")
- Full thinking content displayed in modal when expanded
- Thinking text is complete, formatted, readable
- If empty thinking_steps exist in API (`text=""` or `thinking=null`), they are NOT shown in UI
- Thinking count in UI matches API (excluding empty steps)

**Fail:**
- Thinking section missing when API returns thinking_steps
- Truncated or corrupted thinking text
- Empty text thinking_steps displayed in UI (should be filtered)
- Model name not shown
- Modal doesn't open or shows wrong content
