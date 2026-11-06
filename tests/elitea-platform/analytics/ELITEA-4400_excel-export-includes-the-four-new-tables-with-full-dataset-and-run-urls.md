---
id: ELITEA-4400
title: "Excel export includes Versions, Models, Trigger Sources, and Recent Runs with full dataset, full precision, and Run URLs"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, issue:7033, r-2.0.8, agent-pipeline-analytics, excel-export]
requirements: [EliteaAI/elitea_issues#7033]
---

# ELITEA-4400: Excel export includes Versions, Models, Trigger Sources, and Recent Runs with full dataset, full precision, and Run URLs

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify the Agent/Pipeline detail view's Excel export includes all four new sections (Versions, Models, Trigger Sources, Recent Runs), that the Recent Runs export contains every run in the filtered dataset (not just the visible/paginated page), that a Run URL (or equivalent) column is present and resolves to the correct run page, and that numeric values in the export are full precision rather than display-rounded strings.

**Coverage:**
- All four new sections present in the Excel export
- Recent Runs export row count matches total filtered run count, not just the visible page
- Run URL column present and resolves correctly
- Numeric values exported at full precision, not rounded display strings

## Preconditions

- Logged in to `{{base_url}}`
- An Agent or Pipeline detail view with multi-page Recent Runs data (more runs than fit on one page) and populated Versions, Models, and Trigger Sources tables
- Ability to open and inspect the exported Excel file

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Entity | Agent or Pipeline with multi-page Recent Runs data |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the detail view for the test Agent/Pipeline and note the total run count shown (e.g. via KPI card) for the selected date range | Total run count recorded |
| 2 | Trigger the Excel export for this detail view | Export completes and file downloads successfully |
| 3 | Open the exported file and confirm it contains sections/sheets for Versions, Models, Trigger Sources, and Recent Runs | All four new sections are present in the export |
| 4 | Count the rows in the exported Recent Runs section | Row count matches the total filtered run count noted in step 1, not merely the number of rows visible on the current/paginated screen |
| 5 | Locate the Run URL (or equivalent) column in the exported Recent Runs section and open one of the URLs | URL resolves to the correct corresponding run's Analytics page |
| 6 | Inspect numeric columns (e.g. TOTAL TOKENS, COST) across the exported sections | Values are full precision (e.g. unrounded decimals), not the display-rounded strings shown on screen |

## Expected Final State

The Excel export contains complete Versions, Models, Trigger Sources, and Recent Runs data covering the entire filtered dataset, with working Run URLs and full-precision numeric values.

## Pass/Fail Criteria

**Pass:**
- All four new sections appear in the export
- Recent Runs export row count equals the total filtered run count
- Run URL column is present and each URL opens the correct run page
- Numeric values are exported at full precision

**Fail:**
- Any of the four new sections is missing from the export
- Recent Runs export is limited to the visible/paginated page instead of the full dataset
- Run URL column is missing or resolves incorrectly
- Numeric values are truncated/rounded display strings instead of full precision
