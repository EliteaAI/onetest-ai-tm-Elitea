---
id: ELITEA-0527
title: "Nested Subagent/Subpipeline Runs Add Only +2 Messages to Context [Parametrized]"
priority: high
type: functional
module: context-management
status: ready
execution_type: manual
tags: [feat:context-management, feat:pipelines, feat:agents, issue:4471, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4471]
---
# ELITEA-0527: Nested Subagent/Subpipeline Runs Add Only +2 Messages to Context [Parametrized]

**Module:** Context Management · **Priority:** High · **Type:** Functional

## Preconditions

- Logged in to {{base_url}}
- A parent agent exists that is configured to call 1 or more nested subagents or subpipelines
- In-context budget widget is visible

## Test Data

| # | Scenario | Setup | Expected message delta |
|---|---|---|---|
| 1 | 1 nested subagent | Parent agent calls 1 subagent | +2 |
| 2 | 2 nested subagents | Parent agent calls 2 subagents | +2 |
| 3 | 1 nested subpipeline | Parent agent calls 1 subpipeline | +2 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat or Agent conversation with the parent agent as participant. | Conversation is open. In-context budget is visible. |
| 2 | Note the current message count (N) and token count (T) in the in-context budget. | Baseline N and T are recorded. |
| 3 | Send a single request that triggers the parent agent to call its configured nested subagent(s)/subpipeline(s). Wait for the full run to complete. | Parent agent responds. All nested calls complete internally. |
| 4 | Check the in-context budget. Calculate: new message count − N. | Message delta = exactly +2 (1 user input + 1 agent response), regardless of how many nested subagents/subpipelines ran internally. |
| 5 | Verify the token count delta is proportional to the response content — not multiplied by the number of nested calls. | Token count is not inflated by nested agent/pipeline invocations. |
| 6 | Repeat Steps 1–5 for each remaining row in the test data table. | In every scenario, message delta = +2 and token count is not inflated. |

## Expected Final State

In every scenario, message delta = +2 and token count is not inflated.

## Pass/Fail Criteria

**Pass:** Message count increases by exactly +2 for every parent run, regardless of how many nested subagents/subpipelines were called internally. Token count is not multiplied by nested call count.
**Fail:** Message count increases by +2 × (number of nested agents/pipelines) — e.g. +4 when 2 subagents run — inflating the context incorrectly.
