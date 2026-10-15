---
id: ELITEA-3752
title: "OpenAI compatible toggle on a DIAL Claude-family model"
priority: medium
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:llm-models, dial, openai-compatible, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6707"]
---

# ELITEA-3752: OpenAI compatible toggle on a DIAL Claude-family model

**Module:** model-settings · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the effect of the OpenAI compatible toggle on a Claude-family DIAL model, so its documented recommendation (keep it off for DIAL) is backed by behaviour.

---

## Preconditions

- An AI DIAL credential; a Claude-family DIAL model on Anthropic; an agent with an artifact toolkit.

---

## Test Data

| Field | Value |
|-------|-------|
| Prompts | Plain question; read-and-create tool prompt; a request for a long answer; an image attachment |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | With the toggle off, run all prompts. | All succeed (baseline). |
| 2 | Turn the toggle on and run the plain and tool prompts. | Both succeed. |
| 3 | With the toggle on and reasoning on, run a prompt. | Record whether thinking is applied and shown. |
| 4 | With the toggle on, request a long answer with Max output on Default. | Record whether the answer is cut short. |
| 5 | With the toggle on, send the image prompt. | Record whether the model sees the image. |
| 6 | Select Auto as the model with this Claude model in the pool. | Record whether it is offered/used by Auto. |

---

## Expected Final State

The toggle's effects are known and documented; the default (off) works for every feature.

---

## Pass/Fail Criteria

**Pass:**
- Toggle off: all features work. Toggle on: behaviour recorded for each row.

**Fail:**
- Toggle off fails any feature, or toggle on breaks basic chat or tools.
