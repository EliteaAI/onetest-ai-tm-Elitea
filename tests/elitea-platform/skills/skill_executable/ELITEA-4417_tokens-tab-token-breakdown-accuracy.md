---
id: ELITEA-4417
title: "Verify Tokens tab shows accurate token breakdown by component"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, tokens, data-accuracy]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is on skill run analytics page - Tokens tab
- Run has token usage data

## Test Data

| Field | Value |
|-------|-------|
| Token Components | INPUT TOKENS, OUTPUT TOKENS, CACHE READ, CACHE WRITE |
| Formula | TOTAL TOKENS = INPUT + OUTPUT |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On Tokens tab, observe all token metric cards | Four cards visible |
| 2 | Verify "INPUT TOKENS" card | Displays number of prompt tokens consumed |
| 3 | Verify "OUTPUT TOKENS" card | Displays number of completion tokens generated |
| 4 | Verify "CACHE READ" card | Displays cache read tokens (may be 0 if no caching) |
| 5 | Verify "CACHE WRITE" card | Displays cache write tokens (may be 0 if no caching) |
| 6 | Verify all values are non-negative integers | No negative values, all are integers |
| 7 | Calculate: INPUT + OUTPUT | Sum of input and output tokens |
| 8 | Compare with TOTAL TOKENS card | Calculated sum equals TOTAL TOKENS |
| 9 | Verify cache metrics may be 0 | Cache read/write can be 0 if caching not used |
| 10 | (Backend) Cross-reference with usage_event data | Token counts match DB values |

## Expected Final State

Token breakdown displays:
- INPUT TOKENS: prompt tokens consumed
- OUTPUT TOKENS: completion tokens generated
- CACHE READ: cache read tokens (may be 0)
- CACHE WRITE: cache write tokens (may be 0)
- Formula check: TOTAL TOKENS = INPUT + OUTPUT
- All values are non-negative integers

## Pass/Fail Criteria

**Pass:**
- All four token cards display values
- INPUT TOKENS shows prompt tokens
- OUTPUT TOKENS shows completion tokens
- CACHE READ and CACHE WRITE shown (may be 0)
- TOTAL TOKENS = INPUT + OUTPUT
- All values non-negative integers
- Values match usage_event table

**Fail:**
- Missing token cards
- Incorrect token values
- TOTAL TOKENS ≠ INPUT + OUTPUT
- Negative values present
- Non-integer values
- Data doesn't match usage_event table
