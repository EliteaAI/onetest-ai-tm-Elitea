---
id: ELITEA-2487
title: "Clear all instructions for a personality"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2487: Clear all instructions for a personality

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify user can clear all instructions

## Preconditions

- Nerdy personality has saved instructions

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select "Nerdy" personality | |
| 2 | Delete all text from User instructions | |
| 3 | Observe save confirmation | |
| 4 | Refresh page | |
| 5 | Verify instructions field is empty with placeholder | |

## Expected Results

- Text deletion saves successfully
- Empty state persists after refresh
- Placeholder text appears

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
