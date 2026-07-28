---
id: ELITEA-2488
title: "Set instructions for all personality types"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2488: Set instructions for all personality types

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify all 7 personality types can store unique instructions

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | For each personality (Generic, QA, Nerdy, Quirky, Cynical, None, Bare): Select personality | |
| 2 | Enter unique text: "Instructions for [personality]" | |
| 3 | Observe save confirmation | |
| 4 | Cycle through all personalities again | |
| 5 | Verify each shows its unique instructions | |

## Expected Results

- All 7 types save successfully
- Each retrieves its unique instructions
- No cross-contamination between personalities

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
