---
id: ELITEA-3880
title: "Auto-save when switching personality without typing"
priority: critical
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-3880: Auto-save when switching personality without typing

**Module:** Settings · **Priority:** Critical · **Type:** Functional

**Objective:** Verify changes auto-save when just changing personality selection

## Preconditions

- User logged in, at Settings > AI Personality, Generic personality selected

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify "Generic" is selected in Default persona dropdown | |
| 2 | Select "Nerdy" from Default persona dropdown | |
| 3 | Immediately observe "Settings saved successfully" green banner appears | |
| 4 | Do NOT type any text in User instructions field | |
| 5 | Refresh the browser page | |
| 6 | Navigate to Settings > AI Personality | |
| 7 | Verify "Nerdy" is still selected | |

## Expected Results

- "Settings saved successfully" banner appears immediately after personality selection change
- "Nerdy" remains selected after page refresh
- Personality change is saved automatically without typing instructions

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
