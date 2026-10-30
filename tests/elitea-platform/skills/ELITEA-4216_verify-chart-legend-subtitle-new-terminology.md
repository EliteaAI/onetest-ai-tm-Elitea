---
id: ELITEA-4216
title: "Verify chart legend and subtitle with new terminology"
priority: medium
type: ui
module: analytics-skills
status: ready
execution_type: manual
tags: [feat:analytics, feat:skills, r-2.0.8, nfr:usability]
requirements: [EliteaAI/elitea_issues#7272]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Multiple skills have been used (at least 5 different skills)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/settings/analytics` |
| Tab | Skills |
| Skills | At least 5 skills with varying runs and agent/chat uses |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Navigate to Settings → Analytics → Skills | Skills analytics page loads |
| 2 | Locate "Most Used Skills" chart section | Bar chart displayed below summary cards |
| 3 | Check chart title | Title displays: "Most Used Skills" |
| 4 | Check chart legend | Legend displays: "Runs · Agent & chat uses" |
| 5 | Verify legend has two color indicators | Blue indicator for "Runs", Magenta/Pink indicator for "Agent & chat uses" |
| 6 | Check chart subtitle below the legend | Subtitle reads: "Runs and agent & chat uses on this page" |
| 7 | Verify bars in chart are stacked | Each bar shows two colors: blue (bottom) for Runs, magenta (top) for Agent & chat uses |
| 8 | Hover over a bar in the chart | Tooltip displays skill name with breakdown of runs and agent & chat uses |
| 9 | Verify bar colors match legend | Blue bars match "Runs" legend color, Magenta bars match "Agent & chat uses" legend color |
| 10 | Identify the skill with highest total (runs + agent & chat uses) | Skill appears as tallest bar in chart |
| 11 | Cross-reference with Skill Activity table | Same skill has highest combined values in RUNS and AGENT & CHAT USES columns |
| 12 | Verify chart accurately reflects top 10-15 skills from table | Chart shows most-used skills based on combined metrics |

## Expected Final State

Chart legend and subtitle use "Agent & chat uses" terminology (lowercase after the bullet point). Chart accurately visualizes the top skills based on combined runs and agent/chat uses, with colors matching the legend.

## Pass/Fail Criteria

**Pass:**
- Chart legend uses "Agent & chat uses" terminology (lowercase)
- Chart subtitle is grammatically correct: "Runs and agent & chat uses on this page"
- Legend colors match bar chart colors (blue for Runs, magenta for Agent & chat uses)
- Chart data accurately represents table data
- Hover tooltips display skill name and breakdown
- Stacked bars show runs and uses separately

**Fail:**
- Legend uses old "In-agent uses" terminology
- Subtitle references old terminology
- Legend colors don't match chart colors
- Chart data doesn't match table data
- Missing or incorrect tooltips
- Bars not stacked correctly
