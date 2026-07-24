---
id: ELITEA-2479
title: "Switch between personalities and verify instructions load"
priority: critical
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2479: Switch between personalities and verify instructions load

**Module:** Settings · **Priority:** Critical · **Type:** Functional

**Objective:** Verify switching personalities loads corresponding saved instructions

## Preconditions

- User logged in to Elitea application
- Multiple personalities have saved instructions:
  - Generic: "test1"
  - QA: "test2"
  - Nerdy: "test3"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings > AI Personality | |
| 2 | Select "Generic" from Default persona dropdown | |
| 3 | Verify User instructions field displays "test1" | |
| 4 | Select "QA" from Default persona dropdown | |
| 5 | Verify User instructions field displays "test2" | |
| 6 | Select "Nerdy" from Default persona dropdown | |
| 7 | Verify User instructions field displays "test3" | |
| 8 | Select "Generic" again from dropdown | |
| 9 | Verify User instructions field displays "test1" again | |

## Expected Results

- Step 3: Instructions field shows "test1" for Generic personality
- Step 5: Instructions field immediately updates to "test2" for QA personality
- Step 7: Instructions field immediately updates to "test3" for Nerdy personality
- Step 9: Instructions field returns to "test1" when Generic is re-selected
- No data loss occurs during personality switching
- Each personality loads its specific saved instructions immediately

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
