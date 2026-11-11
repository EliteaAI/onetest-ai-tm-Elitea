---
id: ELITEA-4687
title: "Unknown Model Context Window Falls Back to 128000 Tokens With a Default Indicator"
priority: medium
type: functional
module: context-management
status: draft
execution_type: manual
regression: false
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Reconstruction Note

This case's Part 2 body was missing from the EL-6898-test-cases-draft.md source file (Part 2 jumped directly from ELITEA-4406 to ELITEA-4408, skipping this one) at the time of PR generation. It was reconstructed at full fidelity from Part 1's checklist entry and an earlier-presented version of this case in the review conversation, matching the style of its sibling cases.

## Preconditions

- A custom/OpenAI-compatible model with no known `context_window` metadata is available to add as a chat participant

## Test Data

| Field | Value |
|-------|-------|
| Custom model | A model not present in the configurations catalog's known context_window list |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Add the custom/unknown-window model as a chat participant and send a message. | Response is generated normally. |
| 2 | Open the Context management card. | Total window shows 128,000 with a visible "(default)" label or equivalent fallback indicator next to it. |
| 3 | Switch between Balanced and Full for this chat. | Both modes behave identically (since 128,000 ≤ 272,000), and the "modes are identical" hint is shown. |

## Expected Final State

A model with an unknown context window falls back to a clearly labeled 128,000-token default, and Balanced/Full are shown as equivalent for it.

## Pass/Fail Criteria

**Pass:**
- Total window shows 128,000 with a "(default)"-style indicator for the unknown-window model
- Balanced and Full produce identical values for this model, with the "identical modes" hint shown

**Fail:**
- Total window shows an incorrect or unlabeled fallback value
- No indication is given that 128,000 is a default/fallback rather than the model's real window
