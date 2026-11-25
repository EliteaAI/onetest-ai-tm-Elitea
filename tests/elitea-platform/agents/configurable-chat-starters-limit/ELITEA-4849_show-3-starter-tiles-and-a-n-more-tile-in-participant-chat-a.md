---
id: ELITEA-4849
title: "Show 3 starter tiles and a +N more tile in participant chat and the pipeline Test panel"
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
- Agents with 5 and 10 chat starters and a pipeline with 8 starters exist

## Test Data

| View | Entity | Expected tiles | Popover items |
|------|--------|----------------|---------------|
| Participant chat (real conversation) | Agent, K = 5 | starters 1–3 + "+2 more" | 5 |
| Participant chat (real conversation) | Agent, K = 10 | starters 1–3 + "+7 more" | 10 |
| Pipeline editor → Test panel | Pipeline, K = 8 | starters 1–3 + "+5 more" | 8 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start a conversation with the 5-starter agent as participant | A 2×2 grid: starters 1–3 and the tile "+2 more"; at most 2 rows |
| 2 | Click "+2 more" | The "All chat starters" popover lists all 5 in order |
| 3 | Repeat steps 1–2 with the 10-starter agent | Starters 1–3 + "+7 more"; the popover lists all 10 in order |
| 4 | Open the pipeline and its Test panel | Starters 1–3 + "+5 more"; at most 2 rows |
| 5 | Click "+5 more" | The popover lists all 8 in order |

## Expected Final State

In every chat view, all starters are reachable through the "+N more" tile.

## Pass/Fail Criteria

**Pass:**
- The grid never exceeds 2 rows and shows 3 tiles plus "+(K−3) more"; the popover lists all K in order

**Fail:**
- More than 4 tiles or more than 2 rows are shown, the count in "+N more" is wrong, or starters are missing from the popover
