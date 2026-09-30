---
id: ELITEA-3475
title: "Overview Model Usage Breakdown Table"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, issue:6737, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437, EliteaAI/elitea_issues#6737]
---
# ELITEA-3475: Overview Model Usage Breakdown Table

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Model Usage Breakdown table shows Display Names and consistent data with Usage page.

**Coverage:** Bug #6737 - Model call totals should match between Usage and Analytics pages.

## Preconditions

- Logged into {{base_url}}
- Project has LLM calls with multiple models
- Navigate to Settings → Analytics → Overview

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Scroll to "Model Usage Breakdown" section. | Table visible with title "LLM calls/runs per model". |
| 2 | Verify table columns. | Columns: # (rank), MODEL, CALLS/RUNS, USERS, SHARE. |
| 3 | Verify models show Display Name not raw name. | Shows friendly names (e.g., "Bedrock-GPT-5.6-Luna") not internal identifiers. |
| 4 | Verify CALLS/RUNS shows integer count. | Each model row shows call count as whole number. |
| 5 | Verify USERS shows user count. | Shows number of unique users who used that model. |
| 6 | Verify SHARE shows percentage bar. | Visual progress bar with percentage (e.g., "100.0%"). |
| 7 | Navigate to Usage page, note total calls. | Record total model calls from Usage page. |
| 8 | Compare with Analytics Model breakdown sum. | Sum of model calls in Analytics matches Usage page total (accounting for embedding treatment). |

## Pass/Fail Criteria

**Pass:** Table shows Display Names, all columns populated, totals consistent with Usage page.
**Fail:** Raw model names shown, data mismatch with Usage page, or missing columns.
