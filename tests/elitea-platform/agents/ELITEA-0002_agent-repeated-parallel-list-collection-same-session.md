---
id: ELITEA-0002
title: "[Agent] Repeated Parallel `list_collection` Calls in Same Session — No State Accumulation or Degradation"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:collections, feat:toolkits, eng:backend]
requirements: [EliteaAI/elitea_issues#4959]
---

# ELITEA-0002: [Agent] Repeated Parallel `list_collection` Calls in Same Session — No State Accumulation or Degradation

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that making the same parallel `list_collection` call multiple times within one session without reloading does not accumulate vector store state errors or return inconsistent or degraded results over time.

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)
- Agent configured with 3+ toolkits each having `list_collection` (e.g., GitHub, Jira, Confluence, Artifact)

## Test Data

| Field | Value |
|-------|-------|
| Toolkits | GitHub, Jira, Confluence, Artifact |
| Repetitions | 3 consecutive calls without page reload between them |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent and send: "Call list_collection on ALL toolkits simultaneously in parallel. Do not call them one by one — invoke all at the same time." (1st call) | All toolkits return their collections. No conflict error. |
| 2 | Send the exact same prompt again without reloading the page. (2nd call) | Same collections returned from all toolkits. No error. Results consistent with 1st call. |
| 3 | Send the same prompt one more time. (3rd call) | Results consistent with previous calls. No error or degradation. No state accumulation issues. |

## Expected Final State

All three consecutive parallel `list_collection` invocations across all configured toolkits complete without errors. Each call returns consistent, correct collections with no state accumulation, cross-contamination, or result degradation between repetitions.

## Pass/Fail Criteria

**Pass:**
- All 3 consecutive parallel calls return consistent results with no errors
- No state accumulation or result degradation across calls

**Fail:**
- Any call after the first returns a conflict error or inconsistent/empty results
- Results degrade or differ between calls
