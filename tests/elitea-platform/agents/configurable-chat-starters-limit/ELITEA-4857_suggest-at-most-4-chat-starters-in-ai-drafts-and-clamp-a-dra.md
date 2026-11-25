---
id: ELITEA-4857
title: "Suggest at most 4 chat starters in AI drafts and clamp a draft to the limit"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
known_issues: [elitea_issues#7748]
---

## Preconditions

- User is logged in to `{{base_url}}` as a platform admin
- The original limit is noted (restore it at the end)

## Test Data

| Limit M | Build with AI description | Expected starters |
|---------|---------------------------|-------------------|
| 10 | 9 different descriptions with no starter count asked for (for example a bakery assistant, a hiking planner, a library helper, a chemistry quiz, an onboarding guide, a Lisbon travel helper, internet support, vegetarian recipes, a 10k running coach) | 1–4 each, review "n/10 added." |
| 2 | "…Give it exactly 6 chat starters." | exactly 2, "2/2 added.", no error |
| Draft API | `POST {{base_url}}/api/v2/elitea_core/generate_application_draft/prompt_lib/{{project_id}}` | ≤ M, never 400/422 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set M = 10. For each of the 9 descriptions: Agents → + → Build with AI → Generate, then count the starters on the review step and close without saving | Every draft suggests 1–4 starters, and the counter matches ("n/10 added.") |
| 2 | Set M = 2. Generate a draft that asks for exactly 6 chat starters | The draft is created, not rejected: exactly 2 starters, "2/2 added.", no error |
| 3 | At M = 2, call the draft API with the same description | 200 with at most 2 starters |
| 4 | At M = 2, call the draft API in edit mode for an agent with 8 stored starters ("keep all chat starters") | 200, at most 8 starters (the stored-count ceiling), no 400/422 |
| 5 | At M = 10, call the draft API asking for 12 starters | 200 with at most 10 |
| 6 | Restore the original limit | Restored; nothing was created |

## Expected Final State

AI drafts suggest the default number of starters (≤ 4) and are clamped to the limit instead of being rejected.

## Pass/Fail Criteria

**Pass:**
- All 9 drafts at M = 10 have at most 4 starters
- Over-limit drafts are clamped to M (or the stored count in edit mode) and never rejected

**Fail:**
- Any draft at M = 10 suggests more than 4
- A draft over the limit is rejected or reaches the form with more than M
