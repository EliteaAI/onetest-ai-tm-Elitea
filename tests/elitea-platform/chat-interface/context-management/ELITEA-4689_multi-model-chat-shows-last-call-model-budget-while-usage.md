---
id: ELITEA-4689
title: "Multi-Model Chat Shows Last Call Model Budget While Usage Totals Sum Across Models"
priority: medium
type: integration
module: context-management
status: draft
execution_type: manual
regression: false
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Preconditions

- A chat exists (or can be created) with two participants using two different models with different context windows

## Test Data

| Field | Value |
|-------|-------|
| Participant A | Model 1 with context window W1 |
| Participant B | Model 2 with a different context window W2 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a chat with Participant A (Model 1) and Participant B (Model 2). | Both participants are added successfully. |
| 2 | Send a message addressed to Participant A. | Participant A responds; Context management card reflects Model 1's window (W1). |
| 3 | Send a message addressed to Participant B. | Participant B responds; Context management card now reflects Model 2's window (W2) — the most recent call — not Model 1's. |
| 4 | Inspect the Usage totals (Input/Output tokens, cost). | Totals reflect the combined contribution of BOTH models' calls (summed), consistent with the per-model attribution already covered at the Analytics level by ELITEA-3706/ELITEA-3707. |

## Expected Final State

The Context management card's Total window reflects the most recently called model, while cumulative Usage totals correctly sum contributions across all models used in the chat.

## Pass/Fail Criteria

**Pass:**
- Context management card updates to reflect the last-called model's window after each turn
- Usage totals reflect the sum of both models' contributions, not just one

**Fail:**
- Context management card does not update to the last-called model's window
- Usage totals reflect only one model's contribution, dropping the other
