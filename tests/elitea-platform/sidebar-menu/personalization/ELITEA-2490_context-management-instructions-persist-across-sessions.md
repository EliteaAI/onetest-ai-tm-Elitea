---
id: ELITEA-2490
title: "Context Management instructions persist across sessions"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2490: Context Management instructions persist across sessions

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify per-conversation settings persist after logout/login

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set "Cynical" personality in Context Management for a conversation | |
| 2 | Send message to verify personality applied | |
| 3 | Logout and close browser | |
| 4 | Login and open same conversation | |
| 5 | Check Context Management settings | |

## Expected Results

- Personality remains "Cynical" after login
- Context Management state preserved
- No data loss across sessions

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
