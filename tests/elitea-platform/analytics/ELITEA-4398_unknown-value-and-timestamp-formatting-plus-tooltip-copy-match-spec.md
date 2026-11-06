---
id: ELITEA-4398
title: "Unknown-value labels, timestamp formatting, and contextual tooltip copy match specification exactly across the four new tables"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, issue:7033, r-2.0.8, agent-pipeline-analytics, wording, tooltips]
requirements: [EliteaAI/elitea_issues#7033]
---

# ELITEA-4398: Unknown-value labels, timestamp formatting, and contextual tooltip copy match specification exactly across the four new tables

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that unavailable values display consistently ("—" for missing USER attribution, and the exact "Unknown version" / "Unknown model" / "Unknown" labels per table), that STARTED timestamps follow the same formatting/timezone conventions as other existing Analytics timestamps, and that each of the four new tables exposes an info tooltip whose copy matches the issue specification verbatim, styled consistently with existing Analytics tooltips.

**Coverage:**
- Missing USER attribution shows "—", not blank or an error
- STARTED timestamp format/timezone matches existing Analytics conventions (e.g. Runs by Day, Skill Analytics)
- Exact "Unknown version", "Unknown model", "Unknown" wording per table
- Tooltip copy verbatim match for Versions, Models, Trigger Sources, Recent Runs
- Tooltip styling consistent with existing Analytics tooltips

## Preconditions

- Logged in to `{{base_url}}`
- An Agent or Pipeline with at least one run showing missing USER attribution, if available
- Access to another existing Analytics view with timestamps (e.g. Runs by Day chart or Skill Analytics) for format comparison

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Expected Versions tooltip | "Shows runs, token usage, and estimated cost by the Agent or Pipeline version used during execution." |
| Expected Models tooltip | "Shows models used during execution, including distinct runs, LLM calls, token usage, and estimated cost. A run using multiple models is counted in each applicable model row." |
| Expected Trigger Sources tooltip | "Shows how runs were initiated, with their token usage and estimated cost. Runs without recorded trigger information appear as Unknown." |
| Expected Recent Runs tooltip | "Shows individual runs during the selected period. Select a start time to open that run's Analytics page." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Locate a Recent Runs row with missing USER attribution | USER column shows "—" (not blank, not an error, not "Unknown") |
| 2 | Compare the STARTED timestamp format and timezone in Recent Runs against timestamps in the existing Runs by Day chart or Skill Analytics view | Format and timezone convention match existing Analytics presentation |
| 3 | Locate a row with unattributed version, model, and trigger (where available) | Labels read exactly "Unknown version" (Versions), "Unknown model" (Models), and "Unknown" (Trigger Sources) — matching spec wording precisely |
| 4 | Hover/open the info tooltip for Versions | Tooltip text matches the Versions expected copy verbatim |
| 5 | Hover/open the info tooltip for Models | Tooltip text matches the Models expected copy verbatim |
| 6 | Hover/open the info tooltip for Trigger Sources | Tooltip text matches the Trigger Sources expected copy verbatim |
| 7 | Hover/open the info tooltip for Recent Runs | Tooltip text matches the Recent Runs expected copy verbatim |
| 8 | Compare tooltip visual styling (icon, popover style, font) against an existing Analytics tooltip (e.g. on the KPI cards or Runs by Day) | Styling is visually consistent, not a new/different pattern |

## Expected Final State

All unknown-value labels, timestamp formatting, and tooltip copy across the four new tables match the GitHub issue specification exactly and are visually consistent with existing Analytics conventions.

## Pass/Fail Criteria

**Pass:**
- "—" shown for missing USER; exact "Unknown version"/"Unknown model"/"Unknown" wording used per table
- Timestamp format/timezone matches existing Analytics views
- All four tooltip texts match the specified copy verbatim
- Tooltip styling matches existing Analytics tooltip styling

**Fail:**
- Any wording deviates from the exact spec text (even minor rewording)
- Missing USER shows blank or an error instead of "—"
- Timestamp format/timezone is inconsistent with other Analytics views
- Tooltip styling is visually inconsistent with existing tooltips
