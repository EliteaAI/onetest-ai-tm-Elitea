---
id: ELITEA-1718
title: "Two parallel sub-agents execute concurrently with elapsed time approximately max(A,B)"
priority: critical
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1718: Two Parallel Sub-Agents Execute Concurrently

**Module:** Parallel Sub-Agent HITL · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a parent agent invokes two independent Application sub-agent tools in one LLM turn, they execute concurrently and total wall-clock time is approximately max(A, B), not A + B.

**Applies to:** Both execution modes (In-Process Track 1 and Park+Dispatch Track 2). Parallel execution is the core behavior regardless of mode.

## Preconditions

- Logged in to {{base_url}}
- Parent agent has two Application sub-agent tools: Sub-Agent A (~3–5s) and Sub-Agent B (~3–5s)
- Both sub-agents return distinct results ("result-A" / "result-B")
- Neither sub-agent has sensitive tools (pure execution timing test)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Sub-Agent A response time | ~3–5 seconds |
| Sub-Agent B response time | ~3–5 seconds |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open parent agent chat and send a prompt that triggers both Sub-Agent A and Sub-Agent B in one turn | LLM dispatches both sub-agents in the same response |
| 2 | Observe streaming chips in the UI | Both Sub-Agent A and Sub-Agent B chips appear nearly simultaneously |
| 3 | Wait for both sub-agents to complete | Both "result-A" and "result-B" are present in the parent's synthesis response |
| 4 | Note elapsed time from prompt to final response | Elapsed ~max(A, B) (~5s), NOT A + B (~10s) |

## Expected Final State

Parent response contains both sub-agent results. Total execution time reflects parallel execution.

## Pass/Fail Criteria

**Pass:**
- Both streaming chips appear nearly simultaneously
- Both results present in parent synthesis
- Elapsed time ≈ max(A, B)

**Fail:**
- Chips appear sequentially
- Only one result in parent synthesis
- Elapsed time ≈ A + B
