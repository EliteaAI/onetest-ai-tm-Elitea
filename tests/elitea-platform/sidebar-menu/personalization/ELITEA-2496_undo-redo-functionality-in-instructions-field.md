---
id: ELITEA-2496
title: "Undo/Redo functionality in instructions field"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2496: Undo/Redo functionality in instructions field

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify undo/redo works in User instructions text area

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select "Generic" personality | |
| 2 | Type: "First sentence." | |
| 3 | Type: " Second sentence." | |
| 4 | Press Ctrl+Z to undo | |
| 5 | Verify " Second sentence." is removed | |
| 6 | Press Ctrl+Y to redo | |
| 7 | Verify " Second sentence." returns | |
| 8 | Observe save confirmation | |

## Expected Results

- Undo removes recent text additions
- Redo restores undone text
- Auto-save triggers after undo/redo

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
