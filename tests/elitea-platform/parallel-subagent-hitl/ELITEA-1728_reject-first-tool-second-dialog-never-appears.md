---
id: ELITEA-1728
title: "Rejecting the first sensitive tool prevents second tool dialog from appearing"
priority: critical
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1728: Reject First Sensitive Tool — Second Dialog Never Appears

**Module:** Parallel Sub-Agent HITL · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that rejecting the first sensitive tool terminates the sub-agent flow and prevents the second tool's approval dialog from appearing.

**Applies to:** Mode-agnostic — same as ELITEA-1727, tests sequential multi-interrupt within a single sub-agent.

## Preconditions

- Logged in to {{base_url}}
- Same setup as ELITEA-1727: single sub-agent calls Tool A then Tool B sequentially

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a prompt invoking the sub-agent | Sub-agent dispatched |
| 2 | First approval card appears for Tool A | Card shows Tool A name and arguments |
| 3 | Click Reject/Block for Tool A | Tool A does NOT execute |
| 4 | Observe chat UI | Tool B's approval dialog does NOT appear |
| 5 | Observe parent behavior | Parent receives rejection result cleanly |
| 6 | Verify session | No crash or hang; session remains functional |

## Expected Final State

Tool A not executed. Tool B dialog never appeared. Session functional.

## Pass/Fail Criteria

**Pass:**
- Tool A not executed after rejection
- No Tool B card appears
- Session does not crash or hang

**Fail:**
- Tool A executes despite rejection
- Tool B card appears after Tool A rejected
- Session hangs or crashes
