---
id: ELITEA-1732
title: "Mixed parallel fan-out with one sub-agent and one sub-pipeline both complete and synthesize correctly"
priority: high
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1732: Mixed Parallel — One Sub-Agent + One Sub-Pipeline

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a parent agent invokes one Application sub-agent and one Application sub-pipeline in the same LLM turn, both execute concurrently and the parent synthesizes both results correctly.

**Applies to:** Both execution modes (In-Process Track 1 and Park+Dispatch Track 2).

## Preconditions

- Logged in to {{base_url}}
- Parent agent has one Application sub-agent tool AND one Application sub-pipeline tool
- Sub-agent returns a distinct result (e.g., "agent-result")
- Sub-pipeline returns a distinct result (e.g., "pipeline-result")
- Neither has sensitive tools/HITL nodes

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a prompt that the LLM will delegate to both the sub-agent and the sub-pipeline in one turn | Both dispatched concurrently |
| 2 | Observe streaming chips | Both sub-agent and sub-pipeline chips appear nearly simultaneously |
| 3 | Wait for both to complete | Both results present in parent's synthesis |
| 4 | Verify result attribution | Parent correctly attributes "agent-result" to the sub-agent and "pipeline-result" to the sub-pipeline — no cross-contamination |
| 5 | Note elapsed time | Elapsed ≈ max(agent, pipeline), not sum |

## Expected Final State

Parent response contains both results correctly attributed. Mixed Application types (agent + pipeline) work together in parallel fan-out.

## Pass/Fail Criteria

**Pass:**
- Both sub-agent and sub-pipeline execute concurrently
- Both results present and correctly attributed in parent synthesis
- Elapsed time ≈ max, not sum

**Fail:**
- Only one type executes (the other is skipped or fails)
- Results cross-contaminated between agent and pipeline
- Sequential execution instead of parallel
