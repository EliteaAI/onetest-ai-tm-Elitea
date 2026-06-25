---
id: ELITEA-1723
title: "No stale HITL approval cards remain after all parallel sub-agents complete"
priority: high
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1723: No Stale HITL Cards After All Children Complete

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Functional

**Objective:** Verify that once all parallel sub-agents complete, no orphaned or stale approval cards remain in the chat UI.

**Applies to:** Both execution modes (In-Process Track 1 and Park+Dispatch Track 2). Card cleanup must work regardless of mode.

## Preconditions

- Logged in to {{base_url}}
- Parent agent with two parallel sub-agents, at least one with a sensitive tool

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a prompt triggering both parallel sub-agents | Sub-agents dispatched; approval cards appear as needed |
| 2 | Resolve all approval cards (approve or reject each) | All cards acted upon |
| 3 | Wait for all sub-agents to complete and parent to synthesize | Parent final response appears |
| 4 | Inspect chat message area | No approval cards remain visible |

## Expected Final State

Chat UI shows parent's final response only. Zero lingering approval cards.

## Pass/Fail Criteria

**Pass:**
- No approval cards visible after completion
- Only parent's final response shown

**Fail:**
- Stale cards remain visible
- Ghost cards block or clutter the UI
