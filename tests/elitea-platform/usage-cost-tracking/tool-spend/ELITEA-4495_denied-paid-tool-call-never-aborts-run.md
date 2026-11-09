---
id: ELITEA-4495
title: "Denied paid-tool call never aborts chat, agent, or pipeline run"
priority: critical
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6980]
---
# ELITEA-4495: Denied paid-tool call never aborts chat, agent, or pipeline run

**Module:** Usage Cost Tracking · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm that when a paid-tool monthly limit is reached, only that tool call is refused — the conversation/run continues and the user can keep interacting.

**Coverage:**
- Chat continues after a paid-tool denial
- Agent run completes rather than aborting
- Pipeline (that uses agent) run completes rather than aborting
- No "budget exceeded"-style shutdown message appears for the paid-tool denial

## Preconditions

- A project/member whose paid-tool (e.g. Web Search) monthly limit has been exhausted, or a project pre-configured with a very low limit is available
- User is logged in to `{{base_url}}`

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In a chat with the Web Search module enabled, repeatedly send requests that trigger the paid tool until the monthly limit is reached. | Settings → Usage → Paid Tools progress bar reaches/exceeds 100%. |
| 2 | Send one more request that would trigger the paid tool. | Request is refused for that tool only; no hard failure. |
| 3 | Observe chat behavior. | Chat does not terminate or error out; assistant continues responding (may state the tool is unavailable). |
| 4 | Repeat steps 1–3 in an Agent run. | Agent run completes rather than aborting. |
| 5 | Repeat steps 1–3 in a Pipeline run that uses an agent calling the paid tool at the limit (if accessible). | Pipeline run completes rather than aborting. |
| 6 | Inspect any error/denial message shown. | No message resembling a full "budget exceeded" shutdown (as seen for exhausted LLM budgets) appears. |

## Expected Final State

The conversation/run remains usable after a paid-tool denial; only the specific tool call is refused.

## Pass/Fail Criteria

**Pass:**
- Chat, agent, and pipeline runs all complete after a paid-tool denial
- No full-run abort or "budget exceeded"-style shutdown message appears

**Fail:**
- Any surface (chat/agent/pipeline) terminates or hard-fails upon paid-tool denial
