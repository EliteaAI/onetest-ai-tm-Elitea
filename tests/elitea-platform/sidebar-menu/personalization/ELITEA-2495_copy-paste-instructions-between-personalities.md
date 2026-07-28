---
id: ELITEA-2495
title: "Copy-paste instructions between personalities"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2495: Copy-paste instructions between personalities

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify users can copy instructions from one personality to another

## Preconditions

- QA personality has instructions: "Be technical and testing-focused with detailed examples"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select "QA" personality | |
| 2 | Select all text in User instructions (Ctrl+A) | |
| 3 | Copy text (Ctrl+C) | |
| 4 | Select "Nerdy" personality from dropdown | |
| 5 | Paste text in User instructions (Ctrl+V) | |
| 6 | Observe save confirmation | |
| 7 | Verify QA instructions still intact | |
| 8 | Verify Nerdy has copied instructions | |

## Expected Results

- Copy-paste functionality works
- Original QA instructions unchanged
- Nerdy personality has copied instructions

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
