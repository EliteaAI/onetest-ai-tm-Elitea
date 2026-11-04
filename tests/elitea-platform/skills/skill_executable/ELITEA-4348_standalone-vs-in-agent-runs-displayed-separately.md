---
id: ELITEA-4348
title: "Verify standalone runs and in-agent uses are displayed in separate columns"
priority: critical
type: functional
module: analytics-skills
status: ready
execution_type: manual
tags: [feat:skills, feat:analytics, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6929]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Multiple skills exist with varying usage patterns:
  - Skill A: standalone runs only
  - Skill B: in-agent uses only
  - Skill C: both standalone and in-agent uses

## Test Data

| Field | Value |
|-------|-------|
| Skill A | skill-standalone-only (10 runs, 0 in-agent) |
| Skill B | skill-in-agent-only (0 runs, 20 in-agent) |
| Skill C | skill-mixed-usage (8 runs, 12 in-agent) |
| Analytics URL | `{{base_url}}/settings/analytics?tab=skills` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute Skill A standalone 10 times (no agent usage) | Skill A: 10 standalone runs completed |
| 2 | Execute Skill B in-agent 20 times (no standalone runs) | Skill B: 20 in-agent uses completed |
| 3 | Execute Skill C: 8 standalone runs + 12 in-agent uses | Skill C: 8 runs + 12 in-agent uses completed |
| 4 | Navigate to Settings → Analytics → Skills tab | Skills analytics page loads |
| 5 | Locate Skill A in Skill Activity table | Skill A found |
| 6 | Verify Skill A: "Runs" = 10, "Agent & Chat Uses" = 0 or "—" | Correct: Runs=10, Agent & Chat Uses=0 |
| 7 | Locate Skill B in Skill Activity table | Skill B found |
| 8 | Verify Skill B: "Runs" = 0 or "—", "Agent & Chat Uses" = 20 | Correct: Runs=0, Agent & Chat Uses=20 |
| 9 | Locate Skill C in Skill Activity table | Skill C found |
| 10 | Verify Skill C: "Runs" = 8, "Agent & Chat Uses" = 12 | Correct: Runs=8, Agent & Chat Uses=12 (both columns populated) |
| 11 | Calculate total Skill C invocations: 8 + 12 = 20 | Total = 20 distinct invocations |
| 12 | Click on Skill C to open detail page | Skill C detail page opens |
| 13 | Verify KPI cards: "Runs" = 8, "Agent & Chat Uses" = 12 | KPIs display separate values |
| 14 | Verify trend chart legend shows: "Runs · Agent & chat uses · Cost" | Chart legend distinguishes standalone vs in-agent |
| 15 | Verify trend chart displays two separate lines/bars: one for Runs, one for Agent & Chat Uses | Chart visually separates the two metrics |
| 16 | Check "Trigger Source" breakdown: standalone vs load_skill/mention split | Breakdown shows clear separation |

## Expected Final State

- Standalone runs displayed only in "Runs" column
- In-agent uses displayed only in "Agent & Chat Uses" column
- Skills with both types show both columns populated separately
- No confusion or overlap between the two metrics

## Pass/Fail Criteria

**Pass:**
- Skill A: Runs=10, Agent & Chat Uses=0
- Skill B: Runs=0, Agent & Chat Uses=20
- Skill C: Runs=8, Agent & Chat Uses=12 (separate columns)
- Trend chart and breakdowns distinguish standalone vs in-agent clearly
- No double-counting or misattribution

**Fail:**
- Standalone runs and in-agent uses mixed in a single column
- Incorrect values in "Runs" or "Agent & Chat Uses" columns
- Skill C shows total 20 in one column instead of 8 + 12 separately
- Trend chart does not distinguish standalone vs in-agent
- Confusion between the two metrics
