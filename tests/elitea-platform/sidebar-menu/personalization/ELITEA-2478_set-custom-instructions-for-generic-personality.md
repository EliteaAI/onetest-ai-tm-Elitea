---
id: ELITEA-2478
title: "Set custom instructions for Generic personality"
priority: critical
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2478: Set custom instructions for Generic personality

**Module:** Settings · **Priority:** Critical · **Type:** Functional

**Objective:** Verify user can set and save custom instructions for Generic personality in Settings

## Preconditions

- User logged in to Elitea application
- User has access to Settings > AI Personality page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings > AI Personality | |
| 2 | Select "Generic" from Default persona dropdown | |
| 3 | Enter custom text in User instructions field: "Act as a professional assistant" | |
| 4 | Observe "Settings saved successfully" green banner appears | |
| 5 | Refresh the browser page | |
| 6 | Navigate back to Settings > AI Personality | |
| 7 | Verify "Generic" is selected in Default persona dropdown | |
| 8 | Verify User instructions field displays "Act as a professional assistant" | |

## Expected Results

- Step 4: Green "Settings saved successfully" banner appears after entering text
- Step 7: "Generic" remains selected after page refresh
- Step 8: Instructions "Act as a professional assistant" persist and reload correctly

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
