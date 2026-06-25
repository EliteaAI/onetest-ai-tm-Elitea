---
id: ELITEA-1726
title: "Flat agent with sensitive toolkit — direct HITL approve and reject flows unchanged (regression)"
priority: high
type: regression
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1726: Flat Agent — Direct HITL Unchanged (Regression)

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Regression

**Objective:** Verify that a standard agent (no Application sub-agent tools) with a sensitive toolkit still has unchanged direct HITL approve/reject behavior.

**Applies to:** Mode-agnostic — flat agents do not use sub-agent fan-out; neither execution mode is relevant here.

## Preconditions

- Logged in to {{base_url}}
- Standard agent with a sensitive toolkit directly attached
- NO Application sub-agent tools attached

## Test Data

| Scenario | Action |
|----------|--------|
| A | Approve the sensitive tool |
| B | Reject the sensitive tool |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a prompt triggering the agent to call a sensitive tool directly | Agent dispatches the sensitive tool call |
| 2 | Observe chat UI | Approval card appears with correct tool name and arguments |
| 3a | **[Scenario A]** Click Approve | Tool executes; agent completes normally |
| 3b | **[Scenario B]** Click Reject | Tool does not execute; agent receives rejection |
| 4 | Verify session in both scenarios | No crash or hang; session remains active |

## Expected Final State

Direct agent HITL works identically to pre-feature behavior.

## Pass/Fail Criteria

**Pass:**
- Approval card appears for direct tool call
- Approve → tool executes normally
- Reject → tool not executed, clean rejection
- No crash or hang

**Fail:**
- No approval card for direct tool
- Tool executes despite rejection
- Session hangs or crashes
