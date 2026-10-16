---
id: ELITEA-4057
title: "Analytics run detail matches the predict response for each run"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, usage, run-detail, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6566"]
---

# ELITEA-4057: Analytics run detail matches the predict response for each run

**Module:** analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that for a single agent run, Analytics records the run with the same LLM calls, tool calls, model, tokens, user and agent as the predict response.

---

## Preconditions

- An agent with an artifact toolkit; API access with a personal token.
- Analytics needs about 20-60 s after a response.

---

## Test Data

| Field | Value |
|-------|-------|
| Prompts | A plain question (1 LLM call, no tools) and the read-and-create tool prompt (several LLM calls and tool calls) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the plain prompt through `POST /api/v2/elitea_core/predict/prompt_lib/{project}/{version}` and note `thinking_steps[*].thread_id`. | HTTP 200 with an answer; a thread id is present. |
| 2 | After ~60 s, call `GET /api/v2/usage/analytics_run_detail/prompt_lib/{project}?run_id=<thread_id>`. | The run is found. |
| 3 | Compare: root entity, user, model name, number of LLM calls, tool calls. | All match the predict response and the agent/user that ran it. |
| 4 | Compare input and output tokens with the predict response. | Equal (for Anthropic-family models, analytics input plus cache tokens equals the predict input). |
| 5 | Check every LLM call has tokens, cost and duration. | Present and non-zero for priced models. |
| 6 | Repeat with the tool prompt. | Tool calls listed by name, same as in the predict response. |

---

## Expected Final State

Each run in analytics is an exact record of what the predict response reported.

---

## Pass/Fail Criteria

**Pass:**
- All compared fields match for both prompts.

**Fail:**
- Run missing, wrong user/agent/model, or call/token counts differ.
