---
id: ELITEA-1881
title: "LLM selector — Anthropic models are available and functional (Claude 4.5 Sonnet, Claude 4.6 Sonnet, Claude Haiku 4.5)"
priority: medium
type: functional
module: agents
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1881: LLM selector — Anthropic models are available and functional (Claude 4.5 Sonnet, Claude 4.6 Sonnet, Claude Haiku 4.5)

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that all three specified Anthropic models are present in the LLM selector dropdown, can be selected, saved, and are functional in the embedded chat panel.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent is available.
- Anthropic models are configured in the platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Models to verify | Claude 4.5 Sonnet, Claude 4.6 Sonnet, Claude Haiku 4.5 |
| Test message | Reply only with: CONFIRMED |
| Expected response | CONFIRMED |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page | The agent detail page loads |
| 2 | Click the model selector dropdown | The model selector dropdown opens |
| 3 | Verify all three Anthropic models (Claude 4.5 Sonnet, Claude 4.6 Sonnet, Claude Haiku 4.5) are present in the dropdown | All three models are listed in the dropdown |
| 4 | Select "Claude 4.5 Sonnet" and click Save | Save completes successfully |
| 5 | Open the embedded chat panel and send: "Reply only with: CONFIRMED" | The message is sent |
| 6 | Verify the response contains "CONFIRMED" | The agent response contains "CONFIRMED" |
| 7 | Repeat steps 4–6 for "Claude 4.6 Sonnet" | Claude 4.6 Sonnet is selected, saved, and responds with "CONFIRMED" |
| 8 | Repeat steps 4–6 for "Claude Haiku 4.5" | Claude Haiku 4.5 is selected, saved, and responds with "CONFIRMED" |

---

## Expected Final State

All three Anthropic models are present in the dropdown, can be saved, and produce a valid response in the embedded chat.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All three Anthropic models are available and each responds correctly with "CONFIRMED".

**Fail:**
- Any step produces an error or unexpected result.
- One or more models are missing from the dropdown, or a model fails to produce the expected response.
