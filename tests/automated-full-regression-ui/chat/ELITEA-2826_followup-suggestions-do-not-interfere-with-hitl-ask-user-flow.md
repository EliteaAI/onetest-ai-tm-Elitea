---
id: ELITEA-2826
title: "Chat/Pipelines – Follow-Up Suggestions Do Not Appear During or Interfere With HITL / Ask-User Prompts"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, feat:pipelines, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2826: Chat/Pipelines – Follow-Up Suggestions Do Not Appear During or Interfere With HITL / Ask-User Prompts

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that HITL ("Ask User") flows are entirely unaffected by follow-up suggestions — no suggestion chips appear while an Ask-User prompt is awaiting input, and the Ask-User input/response flow works exactly as before.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- A pipeline or agent configured with a HITL ("Ask User") node/step is available.

---

## Test Data

| Field | Value |
|-------|-------|
| Run | A pipeline/agent run that reaches an Ask-User step |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Start the run and let it reach the Ask-User prompt | Ask-User prompt renders and awaits input; no suggestion chips appear above/near it |
| 2 | Respond to the Ask-User prompt as normal | Ask-User flow proceeds exactly as it did before this feature existed |
| 3 | Let the pipeline/agent finish its full run after HITL resolution | If the final response is suggestion-eligible, chips may appear only after the run has fully completed, never during the Ask-User wait |

---

## Expected Final State

HITL/Ask-User prompts are never accompanied by suggestion chips, and their own input/response mechanics are unchanged by this feature.

---

## Pass/Fail Criteria

**Pass:**
- No suggestion chips render while an Ask-User prompt is active.
- The Ask-User input/response flow behaves identically to pre-feature behavior.

**Fail:**
- Suggestion chips appear during or interfere with the Ask-User prompt.
- The Ask-User flow is altered, delayed, or broken by this feature.
