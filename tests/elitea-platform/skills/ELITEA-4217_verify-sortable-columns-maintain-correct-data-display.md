---
id: ELITEA-4217
title: "Verify sortable columns maintain correct data display"
priority: medium
type: ui
module: analytics-skills
status: ready
execution_type: manual
tags: [feat:analytics, feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7272]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Multiple skills exist with varied metrics (at least 10 skills with different values)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/settings/analytics` |
| Tab | Skills |
| Skills | At least 10 skills with varying RUNS, AGENT & CHAT USES, AGENTS USING, AVG LATENCY, TOKENS, COST values |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Navigate to Settings → Analytics → Skills | Skills analytics page loads |
| 2 | Observe default sort order of Skill Activity table | Table displays skills (check if default sort is by RUNS, LAST USED, or alphabetical) |
| 3 | Click "RUNS" column header | Table sorts by RUNS in descending order (arrow ↓ indicator appears) |
| 4 | Verify skills with highest RUNS values appear at top | Skills ordered correctly by RUNS descending |
| 5 | Click "RUNS" column header again | Table sorts by RUNS in ascending order (arrow ↑ indicator appears) |
| 6 | Verify skills with lowest RUNS values (including 0) appear at top | Skills ordered correctly by RUNS ascending |
| 7 | Click "AGENT & CHAT USES" column header | Table sorts by Agent & Chat Uses in descending order (arrow ↓) |
| 8 | Verify skills with highest agent & chat uses appear at top | Skills ordered correctly by AGENT & CHAT USES descending |
| 9 | Click "AGENTS USING" column header | Table sorts by Agents Using in descending order (arrow ↓) |
| 10 | Verify correct sort order | Skills with most agents using them appear at top |
| 11 | Click "AVG LATENCY" column header | Table sorts by Avg Latency descending (arrow ↓) |
| 12 | Verify skills with "—" in AVG LATENCY column sort appropriately | "—" values appear at bottom (descending) or top (ascending) based on implementation |
| 13 | Click "TOKENS" column header | Table sorts by Tokens descending (arrow ↓) |
| 14 | Click "COST" column header | Table sorts by Cost descending (arrow ↓) |
| 15 | Verify skills with 0 runs showing "—" in COST sort to bottom | "—" values treated as lowest/null in sort |
| 16 | Click "LAST USED" column header | Table sorts by Last Used descending (most recent first) |
| 17 | Verify timestamps are in correct order | Most recent timestamps appear at top |
| 18 | Sort by multiple columns in sequence | Each sort works correctly, updating arrow indicators |
| 19 | Verify data accuracy is maintained during all sorts | Skill names and their associated values stay together correctly |

## Expected Final State

All numeric columns are sortable with visual indicators (↑↓). Skills with "—" values in AVG LATENCY, TOKENS, and COST sort logically (typically at the end). Data integrity is maintained during sorting, and the "AGENT & CHAT USES" column sorts correctly.

## Pass/Fail Criteria

**Pass:**
- All numeric columns are sortable (RUNS, AGENT & CHAT USES, AGENTS USING, AVG LATENCY, TOKENS, COST)
- Sort indicators (arrows ↑↓) display correctly
- Descending sort shows highest values first
- Ascending sort shows lowest values first
- "—" values in AVG LATENCY, TOKENS, COST sort logically
- Data accuracy maintained during sorting (no mismatched skill names/values)
- "AGENT & CHAT USES" column sorts correctly

**Fail:**
- Columns not sortable or sort doesn't work
- Sort indicators missing or incorrect
- Incorrect sort order (ascending/descending reversed)
- Data misalignment during sort (skill names separated from their values)
- "—" values cause sort errors or unexpected ordering
- "AGENT & CHAT USES" column doesn't sort or sorts incorrectly
