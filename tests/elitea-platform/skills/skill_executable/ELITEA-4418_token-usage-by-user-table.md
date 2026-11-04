---
id: ELITEA-4418
title: "Verify Token Usage by User table displays accurate per-user breakdown"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, tokens, tables]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is on skill run analytics page - Tokens tab
- Run has token usage attributed to users

## Test Data

| Field | Value |
|-------|-------|
| Table Columns | USER, TOTAL TOKENS ↓, INPUT TOKENS, OUTPUT TOKENS, CACHE READ, CACHE WRITE, SHARE |
| Sort Order | By TOTAL TOKENS descending |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On Tokens tab, scroll to "Token Usage by User" table | Table is visible |
| 2 | Observe table columns | Headers: USER, TOTAL TOKENS ↓, INPUT TOKENS, OUTPUT TOKENS, CACHE READ, CACHE WRITE, SHARE |
| 3 | Verify all participating users are listed | All users who used tokens in the run appear |
| 4 | Verify token counts per user | Each user shows: total, input, output, cache read, cache write |
| 5 | Calculate per-user: TOTAL = INPUT + OUTPUT | Per-user total equals sum of input and output |
| 6 | Verify SHARE percentage column | SHARE % displayed for each user |
| 7 | Calculate: SHARE % = (user_tokens / total_run_tokens) * 100 | Percentage accurately calculated |
| 8 | Sum all user SHARE percentages | Total of all SHARE percentages = 100% |
| 9 | Verify sort order by TOTAL TOKENS descending (↓) | Users sorted highest tokens to lowest |
| 10 | Cross-reference with usage_event table | Token counts match DB values per user |

## Expected Final State

Token Usage by User table displays:
- All users who participated in the run
- Accurate token counts per user
- TOTAL TOKENS per user = INPUT + OUTPUT tokens
- SHARE % = (user_tokens / total_run_tokens) * 100
- All user SHARE percentages sum to 100%
- Sorted by TOTAL TOKENS descending

## Pass/Fail Criteria

**Pass:**
- All participating users listed
- Token counts per user accurate
- Per-user TOTAL = INPUT + OUTPUT
- SHARE % calculated correctly
- All SHARE percentages sum to 100%
- Table sorted by TOTAL TOKENS descending
- Data matches usage_event table

**Fail:**
- Missing users
- Incorrect token counts
- Per-user TOTAL ≠ INPUT + OUTPUT
- SHARE % calculation wrong
- SHARE percentages don't sum to 100%
- Sort order incorrect
- Data doesn't match usage_event table
