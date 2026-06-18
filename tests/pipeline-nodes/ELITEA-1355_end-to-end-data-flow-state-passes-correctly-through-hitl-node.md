---
id: ELITEA-1355
title: "End-to-End Data Flow: State Passes Correctly Through HITL Node"
priority: high
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1355: End-to-End Data Flow: State Passes Correctly Through HITL Node

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that pipeline state data flows correctly from upstream nodes through the HITL node to downstream nodes without corruption or loss.

**Coverage:**
- Upstream node output is available in HITL USER MESSAGE (F-String interpolation)
- State preserved after Approve action
- Downstream node receives correct combined state

## Preconditions

- Pipeline: LLM Node → HITL Node → Downstream Node (Approve route)
- USER MESSAGE = F-String {{state.llm_output}}
- Pipeline runnable in Chat interface

## Test Data

Pipeline input: Summarize AI trends; Expected state.llm_output: a predictable LLM summary

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Run the pipeline with input 'Summarize AI trends' | Pipeline executes LLM node; state populated with state.llm_output |
| 2 | Pipeline reaches HITL node and pauses | HITL USER MESSAGE displays the LLM output (F-String interpolated correctly) |
| 3 | Click Approve | Pipeline resumes via Approve route |
| 4 | Observe the downstream Approve node execution | Downstream node receives the correct state, including original input + LLM output |
| 5 | Check final pipeline output for completeness | Output includes data from all nodes; no missing or corrupted state |

## Expected Final State

Output includes data from all nodes; no missing or corrupted state

## Pass/Fail Criteria

**Pass:**
- State flows correctly through all nodes including HITL
- No data lost or corrupted at HITL boundary

**Fail:**
- State lost at the HITL boundary
- Wrong or missing data in downstream node
- HITL USER MESSAGE shows wrong state values
