---
id: ELITEA-4053
title: "DIAL model on Azure OpenAI with reasoning shows a non-blocking warning for GPT and Claude families"
priority: medium
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:llm-models, dial, reasoning, ui, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6707", "EliteaAI/elitea_issues#6713", "EliteaAI/elitea_issues#6919"]
---

# ELITEA-4053: DIAL model on Azure OpenAI with reasoning shows a non-blocking warning for GPT and Claude families

**Module:** model-settings · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the form warns, but does not block, when a GPT- or Claude-family DIAL model uses Azure OpenAI with reasoning on, and that no warning is shown for other families.

---

## Preconditions

- A project admin with an AI DIAL credential.

---

## Test Data

| Field | Value |
|-------|-------|
| Models | One GPT-family, one Claude-family and one other-family (e.g. Gemini) DIAL deployment ID |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Configure the Claude-family model with Azure OpenAI and Supports Reasoning on. | A yellow non-blocking warning appears; Save is enabled. |
| 2 | Save. | Saved. |
| 3 | Repeat with the GPT-family model. | Same warning; saved. |
| 4 | Repeat with the other-family model. | No warning; saved. |
| 5 | On the warned Claude model, switch the protocol to Anthropic. | The warning disappears. |
| 6 | Check the warning text for each family. | It recommends the protocol that fits the family (OpenAI for GPT, Anthropic for Claude), not both. |

---

## Expected Final State

The warning guides the admin to the right protocol without blocking the save.

---

## Pass/Fail Criteria

**Pass:**
- Warning shown only for GPT/Claude on Azure with reasoning; never blocks Save; disappears on the right protocol.

**Fail:**
- Save blocked, warning missing for GPT/Claude, shown for other families, or recommending the wrong protocol for the family.
