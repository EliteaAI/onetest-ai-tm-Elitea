---
id: ELITEA-4416
title: "Verify Tokens tab displays accurate total tokens"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, tokens, data-accuracy, bug-check]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is on skill run analytics page
- Run has token usage data in usage_event table
- Run has completed (may have succeeded or failed with errors)

## Test Data

| Field | Value |
|-------|-------|
| Formula | TOTAL TOKENS = Input Tokens + Output Tokens |
| Bug Scenario | Tokens should NOT be zero if Health tab shows LLM calls |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | From Costs tab, click "Tokens" tab | Tokens tab opens and becomes active |
| 2 | Observe "TOTAL TOKENS" card at top | Card displays total token count (numeric value) |
| 3 | Note the total token value | Value is a non-negative integer (e.g., "1000", "0") |
| 4 | Observe individual token metric cards | Four cards visible: INPUT TOKENS, OUTPUT TOKENS, CACHE READ, CACHE WRITE |
| 5 | Note INPUT TOKENS value | Value displayed |
| 6 | Note OUTPUT TOKENS value | Value displayed |
| 7 | Calculate: INPUT + OUTPUT | Manual sum of input and output tokens |
| 8 | Compare calculated sum with TOTAL TOKENS | Calculated sum equals TOTAL TOKENS |
| 9 | **BUG CHECK**: Navigate to Health tab | Health tab opens |
| 10 | **BUG CHECK**: Check if Health tab shows LLM calls | If LLM calls present, tokens should NOT be zero |
| 11 | **BUG CHECK**: Return to Tokens tab and verify values | If Health has LLM calls but Tokens shows all zeros, BUG CONFIRMED |
| 12 | (Backend) Verify usage_event table token counts | UI values match DB sum for this run_id |

## Expected Final State

Tokens tab displays:
- TOTAL TOKENS = Input Tokens + Output Tokens
- Value matches usage_event table sum
- **If Health tab shows LLM calls, tokens must NOT be zero**
- All token counts are accurate

## Pass/Fail Criteria

**Pass:**
- Tokens tab loads successfully
- TOTAL TOKENS = INPUT + OUTPUT
- Values match usage_event table
- **If Health has LLM calls, token counts are NOT zero**
- Data accurate and consistent

**Fail:**
- Tokens tab fails to load
- TOTAL TOKENS ≠ INPUT + OUTPUT
- Values don't match usage_event table
- **BUG: Health shows LLM calls but Tokens tab shows all zeros**
- Data inaccurate or inconsistent

## Notes

**Known Bug (from screenshots)**: Tokens tab may show all zeros (TOTAL: 0, INPUT: 0, OUTPUT: 0, CACHE READ: 0, CACHE WRITE: 0) even when Health tab shows LLM calls with errors. This is a P0 data accuracy bug that must be fixed.
