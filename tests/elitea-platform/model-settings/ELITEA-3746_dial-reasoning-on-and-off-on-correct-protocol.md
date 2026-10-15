---
id: ELITEA-3746
title: "Reasoning can be switched on and off for DIAL models on their correct protocol"
priority: high
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:llm-models, dial, reasoning, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6707", "EliteaAI/elitea_issues#6713", "EliteaAI/elitea_issues#6919"]
---

# ELITEA-3746: Reasoning can be switched on and off for DIAL models on their correct protocol

**Module:** model-settings · **Priority:** High · **Type:** Functional

**Objective:** Verify that on the correct protocol a reasoning-capable DIAL model works with Supports Reasoning both on and off, and that a model without a recognized profile works with reasoning switched on.

---

## Preconditions

- An AI DIAL credential; an agent you can switch between models.
- One reasoning-capable GPT-family and one Claude-family DIAL model on their recommended protocols.
- One DIAL model from a family without a recognized reasoning profile, on Azure OpenAI.

---

## Test Data

| Field | Value |
|-------|-------|
| Prompt | A plain question and the read-and-create tool prompt |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | For the GPT-family model, turn Supports Reasoning on (default effort) and run both prompts. | Both succeed. |
| 2 | Turn Supports Reasoning off and run both prompts. | Both succeed. |
| 3 | Repeat steps 1-2 for the Claude-family model. | Both succeed in both states. |
| 4 | For the model without a recognized profile, turn Supports Reasoning on and run both prompts. | Both succeed; the chosen effort is accepted. |
| 5 | Use a model whose deployment name implies reasoning is built in (a "-reasoning" / "-with-thinking" variant), if available, only to confirm it is not needed: use the base deployment with the toggle instead. | Base deployment + toggle gives the same capability. |

---

## Expected Final State

Reasoning on/off does not break any DIAL model on its correct protocol.

---

## Pass/Fail Criteria

**Pass:**
- Every model works with reasoning on and off on its correct protocol.

**Fail:**
- A model fails or returns an empty reply in either reasoning state on its correct protocol.
