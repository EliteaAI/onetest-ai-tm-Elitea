---
id: ELITEA-1724
title: "Single sub-agent with single sensitive tool — HITL approve flow works (regression)"
priority: high
type: regression
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1724: Single Sub-Agent — Basic HITL Approve (Regression)

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Regression

**Objective:** Verify that the original single-child HITL approve flow remains unchanged after the parallel fan-out changes.

**Applies to:** Mode-agnostic — single sub-agent invocation does not trigger parallel fan-out logic in either mode.

## Preconditions

- Logged in to {{base_url}}
- Agent with one Application sub-agent tool (only one — no parallelism)
- Sub-agent has exactly one sensitive tool

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a prompt triggering the sub-agent's sensitive tool | Sub-agent dispatched |
| 2 | Observe chat UI | Approval card appears with correct tool name and arguments |
| 3 | Click Approve | Sensitive tool executes |
| 4 | Wait for completion | Sub-agent completes; parent receives result |
| 5 | Verify session | Conversation completes normally — no hang or crash |

## Expected Final State

Sensitive tool executed once. Parent received result. Session complete.

## Pass/Fail Criteria

**Pass:**
- Approval card appears correctly
- Tool executes after approval
- Session completes normally

**Fail:**
- No approval card appears
- Tool does not execute after approval
- Session hangs
