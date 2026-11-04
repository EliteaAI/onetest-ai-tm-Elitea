---
id: ELITEA-4419
title: "Verify Token Usage by Model table displays accurate per-model breakdown"
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
- Run used one or more LLM models

## Test Data

| Field | Value |
|-------|-------|
| Table Columns | MODEL, TOTAL TOKENS ↓, INPUT TOKENS, OUTPUT TOKENS, CACHE READ, CACHE WRITE, SHARE |
| Example Models | "test1", "anthropic.claude-sonnet-5-5" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On Tokens tab, scroll to "Token Usage by Model" table | Table visible below Token Usage by User |
| 2 | Observe table columns | Headers: MODEL, TOTAL TOKENS ↓, INPUT TOKENS, OUTPUT TOKENS, CACHE READ, CACHE WRITE, SHARE |
| 3 | Verify all models used in run are listed | All models appear in table |
| 4 | Verify model names match run execution | Model names accurate to execution (not current settings) |
| 5 | Verify token counts per model | Each model shows: total, input, output, cache read, cache write |
| 6 | Calculate per-model: TOTAL = INPUT + OUTPUT | Per-model total equals sum of input and output |
| 7 | Verify SHARE percentage column | SHARE % displayed for each model |
| 8 | Calculate: SHARE % = (model_tokens / total_run_tokens) * 100 | Percentage accurately calculated |
| 9 | Sum all model SHARE percentages | Total of all SHARE percentages = 100% |
| 10 | Verify sort order by TOTAL TOKENS descending (↓) | Models sorted highest tokens to lowest |
| 11 | Cross-reference with usage_event table | Token counts match DB values per model |

## Expected Final State

Token Usage by Model table displays:
- All models used in the run
- Model names match execution (not current skill settings)
- Accurate token counts per model
- TOTAL TOKENS per model = INPUT + OUTPUT
- SHARE % = (model_tokens / total_run_tokens) * 100
- All model SHARE percentages sum to 100%
- Sorted by TOTAL TOKENS descending

## Pass/Fail Criteria

**Pass:**
- All models used in run listed
- Model names accurate to execution
- Token counts per model accurate
- Per-model TOTAL = INPUT + OUTPUT
- SHARE % calculated correctly
- All SHARE percentages sum to 100%
- Table sorted by TOTAL TOKENS descending
- Data matches usage_event table

**Fail:**
- Missing models
- Model names incorrect or show current settings
- Incorrect token counts
- Per-model TOTAL ≠ INPUT + OUTPUT
- SHARE % calculation wrong
- SHARE percentages don't sum to 100%
- Sort order incorrect
- Data doesn't match usage_event table
