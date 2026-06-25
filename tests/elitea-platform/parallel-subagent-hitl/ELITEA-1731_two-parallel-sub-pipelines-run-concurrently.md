---
id: ELITEA-1731
title: "Two parallel sub-pipelines execute concurrently with elapsed time approximately max(A,B)"
priority: high
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1731: Two Parallel Sub-Pipelines Run Concurrently

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a parent agent invokes two independent Application sub-pipeline tools in one LLM turn, they execute concurrently and total wall-clock time is approximately max(A, B), not A + B.

**Applies to:** Both execution modes (In-Process Track 1 and Park+Dispatch Track 2). Parallel execution applies to sub-pipelines the same as sub-agents.

## Preconditions

- Logged in to {{base_url}}
- Parent agent has two Application sub-pipeline tools: Sub-Pipeline A (~3–5s) and Sub-Pipeline B (~3–5s)
- Both sub-pipelines return distinct results
- Neither sub-pipeline has HITL/sensitive nodes (pure execution timing test)

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open parent agent chat and send a prompt that triggers both Sub-Pipeline A and Sub-Pipeline B in one turn | LLM dispatches both sub-pipelines in the same response |
| 2 | Observe streaming chips in the UI | Both Sub-Pipeline A and Sub-Pipeline B chips appear nearly simultaneously |
| 3 | Wait for both sub-pipelines to complete | Both results are present in the parent's synthesis response |
| 4 | Note elapsed time from prompt to final response | Elapsed ~max(A, B) (~5s), NOT A + B (~10s) |

## Expected Final State

Parent response contains both sub-pipeline results. Total execution time reflects parallel execution.

## Pass/Fail Criteria

**Pass:**
- Both streaming chips appear nearly simultaneously
- Both results present in parent synthesis
- Elapsed time ≈ max(A, B)

**Fail:**
- Chips appear sequentially
- Only one result in parent synthesis
- Elapsed time ≈ A + B
