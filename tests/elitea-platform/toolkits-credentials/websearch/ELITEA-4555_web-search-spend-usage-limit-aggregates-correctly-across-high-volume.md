---
id: ELITEA-4555
title: "Web Search spend/usage limit aggregates correctly across high-volume multi-agent calls"
priority: high
type: functional
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- A parent agent is configured to delegate to at least two distinct sub-agents, each with Web Search enabled
- The project's Web Search spend/usage limit is set low enough to be crossed partway through ~30 calls

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Call volume per source | ~10 distinct search queries each |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger a run where the parent delegates to the first sub-agent and prompts it to make ~10 separate Web Search calls | Calls proceed; results return for calls made before any limit is hit |
| 2 | In the same run/conversation, have the parent delegate to a second, different sub-agent and prompt it to make ~10 more Web Search calls | Calls continue to be tracked cumulatively |
| 3 | Still in the same session, directly prompt the parent agent to make ~10 more Web Search calls | Calls continue to be tracked cumulatively |
| 4 | Observe where the limit error is raised relative to the cumulative total across all three sets | Limit is raised once the cumulative total crosses the configured threshold, not before, and not reset per sub-agent |
| 5 | Review the model/agent's handling of the limit event | Model/agent informs the user and the run continues rather than crashing or stalling |
| 6 | Confirm no sub-agent or the parent agent is left in a broken/unresponsive state | All three sources end their portion of the run normally |

## Expected Final State

The spend/usage limit is enforced against the true cumulative total across the parent and both sub-agents, and the run completes without crashing.

## Pass/Fail Criteria

**Pass:**
- Limit triggers at the correct cumulative point across all three call sources combined; run continues and no participant is left broken

**Fail:**
- Limit is tracked separately per sub-agent (triggers too late or not at all), or the run crashes/stalls
