---
id: ELITEA-2499
title: "Concurrent editing from multiple browser tabs"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2499: Concurrent editing from multiple browser tabs

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify behavior when same user edits instructions in multiple tabs

## Preconditions

- Settings > AI Personality page open in TWO browser tabs

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Tab 1: Select "Generic", enter: "Instructions from Tab 1" | |
| 2 | Observe save confirmation in Tab 1 | |
| 3 | In Tab 2: Refresh and verify shows "Instructions from Tab 1" | |
| 4 | In Tab 2: Modify to: "Instructions from Tab 1 edited in Tab 2" | |
| 5 | Observe save confirmation in Tab 2 | |
| 6 | In Tab 1: Refresh and verify latest version | |

## Expected Results

- Last write wins
- Both tabs show same data after refresh
- No data corruption from concurrent editing

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
