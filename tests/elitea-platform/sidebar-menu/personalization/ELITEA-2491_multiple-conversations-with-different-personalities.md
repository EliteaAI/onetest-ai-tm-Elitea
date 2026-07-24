---
id: ELITEA-2491
title: "Multiple conversations with different personalities"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2491: Multiple conversations with different personalities

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify independent personality settings per conversation

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create conversation A with "QA" personality | |
| 2 | Create conversation B with "Nerdy" personality | |
| 3 | Switch between conversations | |
| 4 | Verify each maintains its personality setting | |

## Expected Results

- Conversation A keeps "QA" personality
- Conversation B keeps "Nerdy" personality
- Settings are independent per conversation

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
