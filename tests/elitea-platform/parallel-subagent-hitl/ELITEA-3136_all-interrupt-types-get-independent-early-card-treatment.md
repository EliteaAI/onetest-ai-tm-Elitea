---
id: ELITEA-3136
title: "Sensitive-tool, toolkit-authorization, and explicit HITL pipeline node interrupts all get independent early-card treatment"
priority: critical
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, int:mcp-remote, r-2.0.6, issue:6264]
requirements: [EliteaAI/elitea_issues#6264, EliteaAI/elitea_issues#6072]
---
# ELITEA-3136: All Interrupt Types Get Independent Early-Card Treatment

**Module:** Parallel Sub-Agent HITL · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the new supervisor mode's independent-early-card behavior (ELITEA-3134/3135) is not limited to sensitive-tool-call interrupts — it applies uniformly to a delegated-toolkit-authorization interrupt and to an explicit HITL pipeline node interrupt as well.

**Behavior note:** #6072 (delegated-auth popup UX redesign) governs the *visual content* of the toolkit-authorization card; this test only checks that its *early-independence timing* matches the sensitive-tool case, not its styling/messaging.

## Preconditions

- New supervisor mode enabled
- Three separate staggered fan-out setups available:
  (a) one child reaches a sensitive tool call requiring approval
  (b) one child reaches a toolkit requiring delegated OAuth authorization (e.g. SharePoint/OpenAPI/Remote MCP)
  (c) one child reaches an explicit HITL pipeline node
  — in each case, at least one sibling is still running when the interrupt-triggering child pauses

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Run setup (a): sensitive-tool child pauses while a sibling still runs | Sensitive-tool interrupt card appears independently near the child's own pause time (per ELITEA-3134) |
| 2 | Run setup (b): toolkit-authorization child pauses while a sibling still runs | Toolkit-authorization card appears independently near the child's own pause time, not delayed until the sibling settles |
| 3 | Run setup (c): explicit HITL pipeline node child pauses while a sibling still runs | HITL pipeline node card appears independently near the child's own pause time, not delayed until the sibling settles |
| 4 | For each of (a)/(b)/(c), act on the early card | Only that child resumes; card disappears immediately; sibling unaffected (per ELITEA-3135) |

## Expected Final State

All three interrupt types independently surface per-child without waiting on siblings, and resolve independently when acted on.

## Pass/Fail Criteria

**Pass:** All three interrupt types (sensitive-tool, toolkit-auth, explicit HITL node) show independent early-card timing and independent resume behavior.
**Fail:** Any one of the three interrupt types still waits for siblings before surfacing its card (i.e., falls back to Track 1 aggregate behavior).
