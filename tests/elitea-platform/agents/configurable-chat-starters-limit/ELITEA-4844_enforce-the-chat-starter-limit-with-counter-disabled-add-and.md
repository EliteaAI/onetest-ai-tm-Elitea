---
id: ELITEA-4844
title: "Enforce the chat starter limit with counter, disabled add and tooltips in the agent and pipeline editors"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}` as a platform admin
- The platform limit M is set to 5 (restore the original value at the end)
- There are three entities, set up as in Test Data

## Test Data

| Entity | Starters stored | Expected counter on open |
|--------|-----------------|--------------------------|
| Agent | 4 | "4/5 starters added." |
| Pipeline | 4 | "4/5 starters added." |
| Pipeline created while M was 10 | 8 | "8/5 starters added." (over limit) |
| At-limit tooltip | — | "You have reached the limit of chat starters" |
| Over-limit tooltip | — | "…more starters than the current limit (5). Remove some to add new ones." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | For the agent with 4 and the pipeline with 4: open the editor at Chat Starters | The counter reads "4/5 starters added." and + Starter is enabled |
| 2 | Add a 5th starter | The counter reads "5/5"; + Starter is disabled |
| 3 | Hover + Starter | The at-limit tooltip is shown |
| 4 | Save and reload | The save succeeds and all 5 starters are still there |
| 5 | Open the pipeline with 8 | The counter reads "8/5" in the warning colour (`data-over-limit="true"`); all 8 are listed |
| 6 | Hover + Starter | + Starter is disabled with the over-limit tooltip |
| 7 | Edit the text of one starter and Save | The save succeeds and all 8 are kept |
| 8 | Reset the fixtures to 4 / 4 / 8 and restore the original limit | Cleaned up |

## Expected Final State

Agents and pipelines follow the same limit rules. The over-limit pipeline still has its 8 starters.

## Pass/Fail Criteria

**Pass:**
- Agents and pipelines show the same counter, disabled state and tooltips
- Saving at M, and at an over-limit stored count, succeeds

**Fail:**
- The pipeline editor ignores M or still uses 4
- Adding past M is possible, or an over-limit pipeline can't be saved at its stored count
