---
id: ELITEA-1734
title: "Swarm agent calling pipeline with printer node does not throw GraphInterrupt (regression #5046)"
priority: high
type: regression
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993, EliteaAI/elitea_issues#5046]
---
# ELITEA-1734: Swarm Agent Calling Pipeline With Printer Node — No GraphInterrupt

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Regression

**Objective:** Verify that a swarm-mode agent calling a pipeline containing a printer node completes without throwing a GraphInterrupt — regression fix from #5046.

**Applies to:** Mode-agnostic — this tests swarm-mode pipeline execution, not parallel sub-agent fan-out specifically.

## Preconditions

- Logged in to {{base_url}}
- Swarm-mode agent configured with a pipeline toolkit
- The pipeline contains a printer node (terminal node with `transition: END`)
- Test data from #5046 can be used (Stage project 32, agents 128 + pipeline 125 or equivalent)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Swarm Agent | Agent with swarm mode enabled |
| Pipeline | Pipeline with at least one printer node |
| Reference | #5046 original reproduction data |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the swarm-mode agent in chat | Agent chat interface loaded |
| 2 | Send a prompt that causes the agent to invoke the pipeline containing the printer node | Agent delegates to the pipeline |
| 3 | Observe pipeline execution | Pipeline executes through all nodes including the printer node |
| 4 | Wait for completion | Pipeline completes; printer node outputs are visible |
| 5 | Verify no GraphInterrupt error | No `GraphInterrupt` exception thrown; no error message in chat; session remains functional |
| 6 | Verify parent agent response | Swarm agent synthesizes a normal response using the pipeline output |

## Expected Final State

Pipeline completed successfully including printer node. No GraphInterrupt thrown. Swarm agent produced a normal response.

## Pass/Fail Criteria

**Pass:**
- Pipeline executes through printer node without error
- No GraphInterrupt exception in logs or chat
- Swarm agent completes normally
- Session remains functional

**Fail:**
- GraphInterrupt thrown during pipeline execution
- Error message appears in chat
- Session hangs or crashes at the printer node
- Swarm agent fails to synthesize a response
