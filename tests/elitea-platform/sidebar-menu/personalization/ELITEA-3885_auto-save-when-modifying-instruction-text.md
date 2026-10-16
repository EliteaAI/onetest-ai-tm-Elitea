---
id: ELITEA-3885
title: "Auto-save when modifying instruction text"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-3885: Auto-save when modifying instruction text

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify instruction text changes auto-save

## Preconditions

- Nerdy personality has instructions: "anything random"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select "Nerdy" personality | |
| 2 | Append text: " with detailed explanations" | |
| 3 | Observe save banner | |
| 4 | Navigate away immediately | |
| 5 | Return and verify text includes appended content | |

## Expected Results

- Save banner appears after text modification
- Appended text is preserved
- Auto-save works without explicit save button

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
