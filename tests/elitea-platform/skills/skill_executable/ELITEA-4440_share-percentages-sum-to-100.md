---
id: ELITEA-4440
title: "Verify SHARE percentages sum to exactly 100% in all analytics tables"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, calculations, validation]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is on analytics page with data
- Run has multiple users or models (for meaningful percentage distribution)
- OR run has single user/model (SHARE should be 100.0%)

## Test Data

| Field | Value |
|-------|-------|
| Tables to Check | Cost by User, Cost by Model, Token Usage by User, Token Usage by Model |
| Expected Sum | Exactly 100.0% |

## Steps - Costs Tab

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Costs tab | Costs tab active |
| 2 | Scroll to "Cost by User" table | Table visible |
| 3 | Note all SHARE % values in table | Values recorded |
| 4 | Calculate sum of all SHARE percentages | Manual sum calculation |
| 5 | Verify sum equals 100.0% | Sum = 100.0% |
| 6 | Scroll to "Cost by Model" table | Table visible |
| 7 | Note all SHARE % values | Values recorded |
| 8 | Calculate sum of all SHARE percentages | Manual sum calculation |
| 9 | Verify sum equals 100.0% | Sum = 100.0% |

## Steps - Tokens Tab

| # | Action | Expected Result |
|---|--------|-----------------|
| 10 | Navigate to Tokens tab | Tokens tab active |
| 11 | Scroll to "Token Usage by User" table | Table visible |
| 12 | Note all SHARE % values | Values recorded |
| 13 | Calculate sum of all SHARE percentages | Manual sum calculation |
| 14 | Verify sum equals 100.0% | Sum = 100.0% |
| 15 | Scroll to "Token Usage by Model" table | Table visible |
| 16 | Note all SHARE % values | Values recorded |
| 17 | Calculate sum of all SHARE percentages | Manual sum calculation |
| 18 | Verify sum equals 100.0% | Sum = 100.0% |

## Steps - Single User/Model Case

| # | Action | Expected Result |
|---|--------|-----------------|
| 19 | Test with run having single user | Analytics opens |
| 20 | Verify single user's SHARE = 100.0% | Percentage correct |
| 21 | Test with run having single model | Analytics opens |
| 22 | Verify single model's SHARE = 100.0% | Percentage correct |

## Expected Final State

SHARE percentage validation:
- All SHARE columns sum to exactly 100%
- No rounding errors (99.9% or 100.1%)
- Percentages displayed with consistent decimal places (e.g., "0.0%", "100.0%")
- Single user/model case: SHARE = 100.0%

## Pass/Fail Criteria

**Pass:**
- All four tables: SHARE percentages sum to 100.0%
- No rounding errors
- Consistent decimal places
- Single user/model correctly shows 100.0%

**Fail:**
- SHARE percentages don't sum to 100%
- Rounding errors (99.9%, 100.1%, etc.)
- Inconsistent decimal formatting
- Single user/model not showing 100.0%
- Calculation errors
