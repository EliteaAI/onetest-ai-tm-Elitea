---
id: ELITEA-0804
title: "Nested Sub-Agent Pipeline Triggers Successfully in a Team Project"
priority: critical
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [feat:pipelines, feat:agents, eng:backend, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4489]
---
# ELITEA-0804: Nested Sub-Agent Pipeline Triggers Successfully in a Team Project

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after the fix, a parent agent in a Team project that contains a nested sub-agent with a pipeline executes the full chain successfully from both Chat and Agent page entry points, without the `checkpointer=True cannot be used for root graphs` error.

**Coverage:**
- Chat → Agent → Sub-Agent → Pipeline chain in a Team project
- Agent page → Sub-Agent → Pipeline chain in a Team project
- No `checkpointer` error on either entry point
- Verified with `gpt:5.2` and `anthropic sonnet 4.5`

## Preconditions

- Logged in to {{base_url}}
- Team project exists with: Parent Agent (`CreateABug`) → Sub-Agent (`EnhanceABug`) → Pipeline (`EnhanceABugPipeline`) nested inside sub-agent
- Both `gpt:5.2` and `anthropic sonnet 4.5` models available

## Test Data

- Project type: Team
- Parent agent: `CreateABug`
- Sub-agent: `EnhanceABug`
- Pipeline: `EnhanceABugPipeline`
- Models: `gpt:5.2`, `anthropic sonnet 4.5`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Team project → Agents page. Open the parent agent `CreateABug` and run it from the Agent page using `gpt:5.2`. | Execution starts. Sub-agent `EnhanceABug` is invoked. Pipeline `EnhanceABugPipeline` is triggered. Full chain completes with valid output. No `checkpointer=True cannot be used for root graphs` error appears. |
| 2 | Repeat step 1 using `anthropic sonnet 4.5`. | Same successful result with the second model. No checkpointer error. |
| 3 | Navigate to the Team project → Chat. Create a new conversation. Add `CreateABug` as a participant. Send a prompt that triggers the agent's full execution flow. | Chat → Agent → Sub-Agent → Pipeline chain executes fully. Valid response returned in Chat. No `checkpointer=True cannot be used for root graphs` error appears. |
| 4 | Repeat step 3 using `anthropic sonnet 4.5`. | Same successful result with the second model. Valid response returned with no errors. |

## Expected Final State

Same successful result with the second model. Valid response returned with no errors.

## Pass/Fail Criteria

**Pass:**
- Full chain executes without `checkpointer=True cannot be used for root graphs` on both entry points and both models
- Valid output is returned in all 4 scenarios (Agent page + Chat, gpt:5.2 + anthropic sonnet 4.5)

**Fail:**
- Any scenario produces `checkpointer=True cannot be used for root graphs`
- Pipeline is not triggered in any scenario
- Execution hangs or returns no output
