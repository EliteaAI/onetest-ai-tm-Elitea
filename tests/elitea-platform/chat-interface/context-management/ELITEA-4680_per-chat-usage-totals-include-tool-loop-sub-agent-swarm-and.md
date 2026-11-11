---
id: ELITEA-4680
title: "Per-Chat Usage Totals Include Tool-Loop Sub-Agent Swarm and Summarization Calls"
priority: high
type: integration
module: context-management
status: draft
execution_type: manual
regression: true
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least one configured toolkit (e.g., Artifacts) is available as a chat participant
- A nested sub-agent or swarm-capable agent is available as a chat participant
- Automatic Summarization can be triggered in this chat
- Direct DB/API access to the `audit_events` table (or equivalent) is available, scoped to the test conversation, for the AC17 literal reconciliation step

## Test Data

| Field | Value |
|-------|-------|
| Tool-call request | "List the files in my bucket." (or equivalent toolkit action) |
| Sub-agent request | Any request that triggers the configured sub-agent |
| AC17 reconciliation tolerance | ±1% between chat Usage totals and summed `audit_events` input/output tokens for this conversation's calls |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Note the current Usage totals values in the chat. | Baseline recorded. |
| 2 | Send the tool-call request and wait for completion. | Usage totals (Input/Output tokens, Approx. cost) increase by an amount consistent with the full tool-call round trip, not just the final text answer. |
| 3 | Send the sub-agent request and wait for completion. | Usage totals increase further, accounting for the sub-agent's own LLM call(s), not just the parent agent's final response. |
| 4 | Trigger automatic summarization (e.g., by exceeding the 90% compaction threshold). | Usage totals increase to include the summarization call's own tokens/cost; the summarization call is not excluded from the running totals. |
| 5 | Compare the final Usage totals against the project/agent-level Analytics data for the same time window (cross-reference with ELITEA-3700/3706/3707/3708/4058 figures). | Figures reconcile within a reasonable margin, since both layers share the same underlying pricing/usage utility. |
| 6 | Query `audit_events` (or equivalent) directly via DB/API for all calls attributable to this test conversation, and sum their input/output token columns. Compare that sum against the chat's displayed Usage totals (Input/Output tokens). | The chat's Usage totals match the summed `audit_events` input/output tokens within ±1% — the literal AC17 reconciliation check, independent of the Analytics cross-reference in step 5. |

## Expected Final State

Per-chat Usage totals reflect every LLM call made on behalf of the chat — main turns, tool-loop calls, sub-agent/swarm calls, and summarization calls — and reconcile with both (a) the project/agent-level Analytics figures and (b) the raw `audit_events` token sums within ±1%, per AC17.

## Pass/Fail Criteria

**Pass:**
- Totals increase after tool calls, sub-agent calls, and summarization calls, not just the final visible answer
- Totals reconcile reasonably with project/agent-level Analytics for the same window
- Totals reconcile with the summed `audit_events` input/output tokens for this conversation within ±1%

**Fail:**
- Totals only reflect the final visible answer, undercounting tool/sub-agent/summarization calls
- Totals diverge significantly from the corresponding Analytics figures
- Totals diverge from the summed `audit_events` tokens by more than ±1%
