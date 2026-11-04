---
id: ELITEA-4434
title: "Verify analytics handles skill runs with multiple model changes correctly"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, multi-model, edge-case]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- Skill run switches between multiple models during execution (if supported)
- Example: starts with claude-sonnet-5-5, falls back to claude-haiku-5-5
- OR skill explicitly uses multiple models in sequence

## Test Data

| Field | Value |
|-------|-------|
| Scenario | Skill run using Model A + Model B |
| Example Models | claude-sonnet-5-5, claude-haiku-5-5 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute or locate a skill run that used multiple models | Multi-model run identified |
| 2 | Navigate to analytics page for that run | Analytics page opens |
| 3 | On Costs tab, scroll to "Cost by Model" table | Table visible |
| 4 | Verify all models used are listed | Both/all models appear (e.g., Model A, Model B) |
| 5 | Verify each model has cost breakdown | Per-model costs shown |
| 6 | Verify sum of model costs = TOTAL COST | Calculation correct |
| 7 | Navigate to Tokens tab | Tokens tab opens |
| 8 | Scroll to "Token Usage by Model" table | Table visible |
| 9 | Verify all models used are listed | Both/all models appear |
| 10 | Verify each model has token breakdown | Per-model tokens shown |
| 11 | Verify sum of model tokens = TOTAL TOKENS | Calculation correct |
| 12 | Verify no duplicate counting | Each model counted once |
| 13 | Verify model switching is transparent to user | Clean presentation of multi-model data |

## Expected Final State

Multi-model run handling:
- All models used are listed in Costs and Tokens tabs
- Each model's contribution accurately calculated
- Total cost = sum of all model costs
- Total tokens = sum of all model tokens
- No duplicate counting
- Model switching transparent
- Clean data presentation

## Pass/Fail Criteria

**Pass:**
- All models used listed in both tabs
- Per-model breakdowns accurate
- Totals match sums
- No duplicate counting
- Clear presentation
- Data accurate

**Fail:**
- Missing models
- Incorrect per-model breakdowns
- Totals don't match sums
- Duplicate counting detected
- Confusing presentation
- Data inaccurate
