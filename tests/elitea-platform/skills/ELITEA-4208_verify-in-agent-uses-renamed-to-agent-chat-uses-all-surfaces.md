---
id: ELITEA-4208
title: "Verify 'In-agent uses' renamed to 'Agent & Chat Uses' across all surfaces"
priority: critical
type: ui
module: analytics-skills
status: ready
execution_type: manual
tags: [feat:analytics, feat:skills, r-2.0.8, nfr:usability]
requirements: [EliteaAI/elitea_issues#7272]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Skills analytics data is available
- At least one skill has been used in agents/chats

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/settings/analytics` |
| Tab | Skills |
| Skills | Skills with various usage patterns (runs, agent uses, chat uses) |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Navigate to Settings → Analytics → Skills tab | Skills analytics page loads |
| 2 | Check the summary card labels (4 cards at top) | Cards display: "SKILL RUNS", "SKILLS USED", "AGENT & CHAT USES", "SKILL RUN COST" |
| 3 | Check "Most Used Skills" chart legend | Legend displays: "Runs · Agent & chat uses" |
| 4 | Check chart subtitle below the legend | Subtitle reads: "Runs and agent & chat uses on this page" |
| 5 | Check Skill Activity table column headers | Table includes column header: "AGENT & CHAT USES" (not "In-Agent Uses") |
| 6 | Click on any skill name in the table | Skill detail page opens |
| 7 | Check skill detail summary cards | Card displays: "AGENT & CHAT USES" |
| 8 | Check skill detail trend chart legend | Legend displays: "Runs · Agent & chat uses · Cost (USD)" |
| 9 | Scroll to Versions section | Headers show: "Runs · Agent & Chat Uses" |
| 10 | Navigate to Analytics → Guide tab | Guide page loads |
| 11 | Find Skills Tab entry in Guide | Entry shows "Agent & Chat Uses" (not "In-agent uses") |
| 12 | Go back to Skills tab → Export to Excel | Download completes |
| 13 | Open exported Excel file → Check column headers | Excel column shows: "Agent & Chat Uses" (not "In-Agent Uses") |

## Expected Final State

All 12 locations consistently use "Agent & Chat Uses" terminology. No instances of "In-agent uses" remain in the UI or Excel export.

## Pass/Fail Criteria

**Pass:**
- All 12 locations consistently use "Agent & Chat Uses" terminology
- No instances of "In-agent uses" remain in the UI
- Excel export matches UI terminology
- Terminology is consistent across Skills tab, Skill detail page, and Guide

**Fail:**
- Any instance of "In-agent uses" found in UI
- Excel export uses old terminology
- Inconsistent naming across different surfaces
