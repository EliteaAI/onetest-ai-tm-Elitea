---
id: ELITEA-2492
title: "Personality dropdown shows all types with descriptions"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2492: Personality dropdown shows all types with descriptions

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify dropdown displays all 7 personality types

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click Default persona dropdown | |
| 2 | Verify all types listed with descriptions: Generic, QA, Nerdy, Quirky, Cynical, None, Bare | |
| 3 | Select each type and verify selection works | |

## Expected Results

- All 7 types visible with descriptions
- Selection mechanism works for all types

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
