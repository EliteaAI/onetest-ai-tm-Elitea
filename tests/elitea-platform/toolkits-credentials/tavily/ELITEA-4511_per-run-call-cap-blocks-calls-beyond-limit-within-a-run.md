---
id: ELITEA-4511
title: "Verify Per Run Call Cap blocks further tool calls once the limit is reached within a single run"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit exists with a valid credential and a configurable Per Run Call Cap, attached to an agent capable of multiple tool calls per run

## Test Data

| Field | Value |
|-------|-------|
| Per Run Call Cap | 2, then 1, then 10 (default) |
| Prompt | Single message asking for 3+ separate web searches |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set Per Run Call Cap to 2 and ask the agent, in one message, to perform 3 separate searches | First 2 calls succeed; the 3rd+ is refused with a clear message; the agent's response still completes without the run crashing |
| 2 | Set Per Run Call Cap to 1 and repeat with 2 searches in one message | The 2nd call is refused immediately — the cap is enforced starting at the first call over the limit |
| 3 | Start a brand-new conversation/run after step 2 and request a search | The call succeeds — the cap resets per run, not cumulatively across runs |
| 4 | Set Per Run Call Cap to 10 (default) and have a normal multi-search conversation (a handful of searches) | The cap is never hit unexpectedly during normal use |

## Expected Final State

Per Run Call Cap is confirmed as a real, per-run-scoped enforced ceiling with a clear denial message.

## Pass/Fail Criteria

**Pass:**
- Calls beyond the cap are refused with a clear message
- The run continues
- The cap resets on a new run

**Fail:**
- A call beyond the cap succeeds
- The run crashes instead of continuing
- The cap persists across separate runs
