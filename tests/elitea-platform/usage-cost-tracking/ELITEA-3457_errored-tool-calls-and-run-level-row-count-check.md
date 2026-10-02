---
id: ELITEA-3457
title: "Errored tool calls record is_error=true with no tokens/cost; nested tool calls inherit parent run_id; row count equals N+M per run"
priority: high
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, error-handling, tool-calls]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6572"]
---

# ELITEA-3457: Errored tool calls record is_error=true with no tokens/cost; nested tool calls inherit parent run_id; row count equals N+M per run

**Module:** usage-cost-tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify that a failed tool call produces a `usage_event` row with `event_type='tool'`, `is_error=true`, and a real `duration_ms` (token/cost columns NULL by design), that nested/sub-agent tool calls inherit the parent run's `run_id` and attribution, and that a run with N LLM calls and M tool calls produces exactly N+M rows sharing one `run_id`.

---

## Preconditions

- Logged in to {{base_url}}.
- An agent with at least one toolkit attached, and a way to force a tool-call failure (e.g. invalid tool parameters, unreachable integration endpoint).
- An agent/pipeline run that is known to make a specific, countable number of LLM calls (N) and tool calls (M), including at least one nested/sub-agent tool call if the test environment supports sub-agents.

---

## Test Data

| Field | Value |
|-------|-------|
| Forced tool failure | Any reproducible tool-call failure (bad params, unreachable integration) |
| Known run shape | N LLM calls + M tool calls, recorded before the run |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger a tool call that fails (e.g. via an agent configured to call a misconfigured toolkit action). | Tool call fails; agent surfaces the failure. |
| 2 | Inspect the resulting `usage_event` row. | `event_type='tool'`, `is_error=true`, real `duration_ms` present, token/cost columns are NULL. |
| 3 | Run an agent flow that includes a nested/sub-agent tool call. | Sub-agent tool call executes as part of the parent run. |
| 4 | Inspect the nested tool call's row. | `run_id` and attribution match the **parent** run, not an independent re-attribution. |
| 5 | Run a flow with a known N LLM calls + M tool calls. | Run completes. |
| 6 | Count the `usage_event` rows sharing that run's `run_id`. | Exactly N+M rows are present. |

---

## Expected Final State

Tool-call failures are recorded correctly with no tokens/cost; nested tool calls share the parent's `run_id`; row counts per run match N+M exactly.

---

## Pass/Fail Criteria

**Pass:**
- Failed tool-call row matches the described shape exactly.
- Nested tool call's `run_id`/attribution matches the parent run.
- Row count for the known run equals N+M.

**Fail:**
- Tool-call row has non-NULL token/cost columns, or is missing `is_error`/`duration_ms`.
- Nested tool call is independently (re-)attributed instead of inheriting the parent run.
- Row count does not equal N+M (missing or duplicated rows).
