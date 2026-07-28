---
id: ELITEA-2497
title: "Maximum character limit for instructions"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2497: Maximum character limit for instructions

**Module:** Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify if there's a maximum character limit and how it's handled

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select "Bare" personality | |
| 2 | Attempt to enter very long text (5000+ characters) | |
| 3 | Observe if character counter or limit warning appears | |
| 4 | Attempt to save | |
| 5 | Verify system behavior (limit warning or successful save) | |
| 6 | Refresh page | |
| 7 | Verify saved text matches entered text (or truncated at limit) | |

## Expected Results

- If limit exists: clear warning message and counter displayed
- If no limit: very long text saves successfully
- User informed of any limits before data loss

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
