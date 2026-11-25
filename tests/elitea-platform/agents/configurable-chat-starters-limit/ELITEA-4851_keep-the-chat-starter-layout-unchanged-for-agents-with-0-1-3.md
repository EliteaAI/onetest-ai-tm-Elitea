---
id: ELITEA-4851
title: "Keep the chat starter layout unchanged for agents with 0, 1, 3 and 4 starters"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Agents with 0, 1, 3 and 4 chat starters exist

## Test Data

| Starters K | New-chat empty state | Participant chat / Test panel |
|------------|----------------------|-------------------------------|
| 0 | no starters area | no starters area |
| 1 | 1 row | 1 tile |
| 3 | 3 rows | 3 tiles in one row |
| 4 | 4 rows | 4 tiles in a 2×2 grid |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | For each agent in Test Data: open a new chat and select it | K rows in order; no "Show N more" link |
| 2 | Click a visible row (K ≥ 1) | Its text fills the composer, as before #7322 |
| 3 | Start a conversation with the agent as participant | K tiles in order in the layout from Test Data; no "+N more" tile |
| 4 | Click a visible tile (K ≥ 1) | Its text fills the composer and the tiles hide, as before #7322 |
| 5 | Open the agent's Test panel | K tiles in order; no "+N more" tile |
| 6 | Click a visible tile (K ≥ 1) | Its text fills the composer |

## Expected Final State

Agents with up to 4 starters look and behave as they did before #7322.

## Pass/Fail Criteria

**Pass:**
- No "Show N more" or "+N more" control for K ≤ 4; layout and click behaviour match the pre-#7322 baseline

**Fail:**
- A "more" control appears, the layout changes, or a click behaves differently than before
