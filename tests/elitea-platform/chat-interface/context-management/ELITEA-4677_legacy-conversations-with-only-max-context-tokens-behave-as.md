---
id: ELITEA-4677
title: "Legacy Conversations With Only Max Context Tokens Behave as Balanced Without Errors"
priority: critical
type: regression
module: context-management
status: draft
execution_type: manual
regression: true
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A conversation exists (or can be simulated via API/DB) whose stored context strategy only has the legacy `max_context_tokens` field and no `context_window_mode`

## Test Data

| Field | Value |
|-------|-------|
| Legacy conversation | Created before this feature shipped, `meta.context_strategy.max_context_tokens` set, no `context_window_mode` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the legacy conversation. | Conversation opens without errors; the Context management widget renders normally. |
| 2 | Inspect the Window mode shown in the widget. | Window mode shows "Balanced". |
| 3 | Inspect the budget numbers (Total window, available window). | Values are computed via the Balanced calculation (capped at 272,000 or the model's window, whichever is smaller) — not derived from the old legacy numeric value. |
| 4 | Without saving any new context settings, reload the conversation and re-inspect its stored strategy (via API if available). | The legacy `max_context_tokens` value is still present and has NOT been silently rewritten by simply opening the conversation. |
| 5 | Explicitly save a new context strategy (e.g., toggle Full then back to Balanced and Save). | After this explicit save, the stored strategy now includes `context_window_mode`. |

## Expected Final State

Legacy conversations open and compute their budget correctly as Balanced, without errors, and without the legacy field being silently overwritten until the user explicitly saves new settings.

## Pass/Fail Criteria

**Pass:**
- Legacy conversation opens without errors
- Window mode defaults to Balanced and budget values follow the Balanced calculation
- The legacy numeric field is not silently rewritten until an explicit save occurs

**Fail:**
- Opening the legacy conversation throws an error or fails to render the widget
- Budget values are computed from the old legacy number instead of Balanced
- The stored strategy is silently mutated just by opening the conversation
