---
id: ELITEA-2489
title: "Long instruction text handling"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2489: Long instruction text handling

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify system handles 1000+ character instructions

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select "Bare" personality | |
| 2 | Enter 1000+ character text | |
| 3 | Observe save confirmation | |
| 4 | Refresh and verify full text preserved | |
| 5 | Use "Full screen view" if available | |
| 6 | Verify text displays correctly in full screen | |

## Expected Results

- Long text saves without error
- No character truncation
- Full screen mode works properly

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
