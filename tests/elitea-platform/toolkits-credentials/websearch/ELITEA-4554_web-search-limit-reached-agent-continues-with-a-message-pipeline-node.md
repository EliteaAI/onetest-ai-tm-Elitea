---
id: ELITEA-4554
title: "Web Search limit reached: agent continues with a message, pipeline node continues with an error outcome"
priority: high
type: functional
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- Web Search spend/usage limit is configured low enough to be hit quickly (test environment equivalent)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Chat prompt | "Run 15 searches about [topic]" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In a chat/agent with Web Search enabled, send the test prompt requesting enough searches to exceed the configured limit | Model's response explicitly tells the user the limit was reached for the blocked portion |
| 2 | Review the response for the portion that succeeded before the limit | Results are still returned for the successful portion |
| 3 | Send a follow-up message in the same conversation | Conversation remains usable; no crash or stuck state |
| 4 | In a pipeline with a node using Web Search, configure the node/limit so the call exceeds the limit during a run | Pipeline run does not stop/fail entirely at that node |
| 5 | Inspect the node's outcome | Node surfaces an error/limit outcome and the pipeline continues to subsequent steps (or completes) |

## Expected Final State

Both the chat/agent run and the pipeline run remain alive and usable after the limit is hit, each surfacing the limit condition without halting.

## Pass/Fail Criteria

**Pass:**
- Agent informs the user and the conversation continues; pipeline node yields an error outcome and the run continues

**Fail:**
- The agent conversation becomes unusable, or the pipeline run halts/fails entirely at the limited node
