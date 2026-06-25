---
id: ELITEA-1725
title: "Single sub-agent with single sensitive tool — HITL reject flow works (regression)"
priority: high
type: regression
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1725: Single Sub-Agent — Basic HITL Reject (Regression)

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Regression

**Objective:** Verify that the original single-child HITL reject flow remains unchanged after the parallel fan-out changes.

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
| 3 | Click Reject/Block | Sensitive tool does NOT execute |
| 4 | Observe parent behavior | Parent receives rejection result cleanly |
| 5 | Verify session | Session does not hang or crash; conversation remains functional |

## Expected Final State

Tool not executed. Parent received rejection result. Session functional.

## Pass/Fail Criteria

**Pass:**
- Tool not executed after rejection
- Parent receives clean rejection
- Session remains active

**Fail:**
- Tool executes despite rejection
- Session hangs or crashes
