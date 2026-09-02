---
id: ELITEA-3141
title: "Anthropic and OpenAI message ordering remains valid across a partial-resume conversation"
priority: medium
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6, issue:6264]
requirements: [EliteaAI/elitea_issues#6264]
---
# ELITEA-3141: Message Ordering Remains Valid Across Partial Resume

**Module:** Parallel Sub-Agent HITL · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that after a fan-out where one child was resumed early (independently, before its siblings settled), the resulting conversation's message history remains a valid, correctly-ordered sequence for both Anthropic-style and OpenAI-style model configurations — no malformed or out-of-order tool-call/tool-result pairing.

## Preconditions

- New supervisor mode enabled
- One agent/pipeline configured with an Anthropic-family model, another with an OpenAI-family model, both able to reproduce the staggered-fan-out-with-early-resume scenario from ELITEA-3134/3135
- Access to inspect the raw message history (e.g. via API/trace) after the conversation completes

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Under the Anthropic-model agent, run the staggered fan-out; resume the fast child early while the slow sibling is still running; let the slow sibling settle later | Conversation completes without errors |
| 2 | Inspect the raw message history | Tool-call and tool-result messages are correctly paired and ordered per Anthropic's message-format requirements; no missing/duplicated entries from the partial resume |
| 3 | Repeat steps 1–2 under the OpenAI-model agent | Conversation completes without errors; message history is valid per OpenAI's message-format requirements |
| 4 | Send a follow-up message in each conversation after the fan-out completes | Model responds normally, confirming the history it received was well-formed (no downstream API rejection due to malformed history) |

## Expected Final State

Both model families produce valid, correctly-ordered message histories despite the early/independent partial-resume sequencing introduced by the new supervisor mode.

## Pass/Fail Criteria

**Pass:** Message history is valid and correctly ordered for both model families; follow-up messages succeed normally.
**Fail:** Message history is malformed/out-of-order, or a follow-up message triggers an API-level rejection due to invalid history structure.
