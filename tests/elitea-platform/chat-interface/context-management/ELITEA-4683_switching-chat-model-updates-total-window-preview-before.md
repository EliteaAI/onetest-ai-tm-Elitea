---
id: ELITEA-4683
title: "Switching Chat Model Updates Total Window Preview Before Backend Confirmation"
priority: high
type: functional
module: context-management
status: draft
execution_type: manual
regression: false
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An active chat conversation exists, with at least two models with different context windows available in the model selector

## Test Data

| Field | Value |
|-------|-------|
| Model 1 | Current active model |
| Model 2 | A different model with a different context window size |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the chat and note the current Total window value in the Context management card for Model 1. | Baseline value recorded. |
| 2 | Switch the active model to Model 2 via the model selector, without sending a message yet. | Context management card's Total window updates immediately to reflect Model 2's known context window (client-side preview), before any backend round trip. |
| 3 | Send a message using Model 2. Wait for the response. | After the response completes, the Total window value is confirmed by the backend-resolved value, matching the preview for a known model. |

## Expected Final State

Switching models updates the Total window preview immediately in the UI, and the backend-resolved value after the next response matches that preview for a known model.

## Pass/Fail Criteria

**Pass:**
- Total window updates immediately upon model switch, before sending a message
- The backend-confirmed value after the response matches the earlier preview

**Fail:**
- Total window does not update until after a message is sent
- The backend-confirmed value diverges from the preview for a known model without explanation
