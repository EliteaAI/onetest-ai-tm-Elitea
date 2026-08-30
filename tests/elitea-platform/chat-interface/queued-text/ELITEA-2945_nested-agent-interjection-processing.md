---
id: ELITEA-2945
title: "Verify interjections during nested agent get separate responses"
priority: critical
type: functional
module: interjections
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, nested-agent, bug-6464]
requirements: [EliteaAI/elitea_issues#6115, EliteaAI/elitea_issues#6464]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Parent agent configured to call nested agent
- Nested agent has sufficient execution time to allow interjections

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Parent Agent | Agent with nested agent tool configured |
| Interjection 1 | "Summarize the output" |
| Interjection 2 | "Add more detail" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send message that triggers nested agent execution | Parent agent starts, nested agent is invoked |
| 2 | While nested agent runs, send first interjection | Message queued in "Waiting messages" area |
| 3 | Send second interjection | Second message queued, count shows 2 |
| 4 | Wait for initial response to complete | Nested agent completes, parent returns response |
| 5 | Observe queued message processing | Each interjection processed separately |
| 6 | Verify response display | Two distinct responses visible |

## Expected Final State

- Both interjections have individual request-response pairs
- Responses NOT combined into single output
- Each response visible in interaction window

## Pass/Fail Criteria

**Pass:**
- Interjections remain queued during nested agent execution
- Each interjection gets separate response after initial completes
- Request-response pairs displayed individually

**Fail:**
- Interjections combined into single output
- Only one response generated for both interjections
- Responses merged or missing
