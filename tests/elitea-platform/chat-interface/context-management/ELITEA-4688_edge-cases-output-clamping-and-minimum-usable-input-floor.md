---
id: ELITEA-4688
title: "Edge Cases: Output-Clamping and Minimum Usable-Input Floor"
priority: medium
type: functional
module: context-management
status: draft
execution_type: manual
regression: false
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Merge Note

Merges former draft cases "Custom max_tokens larger than max_output_tokens is clamped" and "Very small model context window keeps usable input above zero" — both are boundary conditions on the same output-reservation formula (one from above, one from below).

## Preconditions

- A model with a documented `max_output_tokens` value is available as a chat/agent participant, with custom max completion tokens configurable
- A model (or custom model configuration) with a very small context window (e.g., ~8,000 tokens) is available as a chat participant

## Test Data

| Field | Value |
|-------|-------|
| Model's documented max_output_tokens | e.g., 16,000 |
| Custom max_tokens configured | A value larger than the model's max_output_tokens, e.g., 50,000 |
| Small-window model | ~8,000 token context window |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Configure the chat/agent's model settings with a custom max completion tokens value larger than the model's documented max_output_tokens. | Setting is accepted by the UI (no immediate validation error expected here, since clamping happens in the budget calculation). |
| 2 | Open the Context management card. | "Minimum output allowance" (reserved output) shows the model's actual max_output_tokens value (clamped), not the larger custom value entered. The usable input / available window values are consistent with this clamped figure. |
| 3 | Select or configure the small-window model (~8,000 tokens) as a chat participant and send a message. | Response is generated normally, no crash. |
| 4 | Open the Context management card for this small-window model. | Total window, Safety margin, and Minimum output allowance are all displayed with sensible values; the resulting usable/available input is greater than zero. |
| 5 | Confirm no error state is shown in either widget. | No error, crash, NaN, or negative value is displayed anywhere in the Context management card for either scenario. |

## Expected Final State

The budget calculation clamps an oversized custom max_tokens setting to the model's actual max_output_tokens, and a very small context window still produces a valid, positive usable input — with no errors in the UI in either case.

## Pass/Fail Criteria

**Pass:**
- Minimum output allowance reflects the model's actual max_output_tokens, not an oversized custom value; usable input / available window are consistent with the clamped value
- Usable/available input is a positive, non-zero number for the small-window model
- No error, crash, or invalid (NaN/negative) value appears in either widget

**Fail:**
- The budget uses the oversized custom value directly, producing an incorrect (too-small or negative) usable input
- Usable input is zero, negative, or NaN for the small-window model, or the widget crashes/shows an error state
