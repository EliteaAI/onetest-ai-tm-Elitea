---
id: ELITEA-1727
title: "Sub-agent calling two distinct sensitive tools sequentially shows two sequential approval dialogs"
priority: critical
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1727: Sub-Agent Calls Two Distinct Sensitive Tools Sequentially

**Module:** Parallel Sub-Agent HITL · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a single sub-agent calls two distinct sensitive tools (Tool A then Tool B), each triggers its own sequential approval dialog — the while-loop multi-interrupt fix from PR #199.

**Applies to:** Mode-agnostic — this tests sequential multi-interrupt within a single sub-agent, not parallel fan-out between multiple sub-agents. Behavior is the same in both execution modes.

## Preconditions

- Logged in to {{base_url}}
- Agent with one Application sub-agent tool (single sub-agent, not parallel)
- Sub-agent configured to call Tool A (`create_issue`, sensitive) then Tool B (`delete_issue`, sensitive, different name) in sequence

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a prompt invoking the sub-agent | Sub-agent dispatched |
| 2 | Execution pauses at Tool A | First approval card shows **Tool A** name (`create_issue`) and arguments; Tool A has NOT run |
| 3 | Click Approve for Tool A | Tool A executes exactly once |
| 4 | Execution pauses at Tool B | Second approval card shows **Tool B** name (`delete_issue`) — NOT a stale copy of Tool A; Tool B has NOT run |
| 5 | Click Approve for Tool B | Tool B executes exactly once |
| 6 | Verify final state | Both tools ran exactly once; execution completes |

## Expected Final State

Two sequential dialogs appeared with distinct, correct tool names. Both tools executed exactly once.

## Pass/Fail Criteria

**Pass:**
- First card shows Tool A name/arguments
- After approving Tool A, second card shows Tool B name (not stale copy)
- Both tools executed exactly once

**Fail:**
- Only one card total
- Second card shows stale Tool A name
- Either tool executes without approval or runs more than once
