---
id: ELITEA-3830
title: "Verify 'Agent & Chat Uses' terminology across all Skills Analytics surfaces"
priority: critical
type: ui
module: analytics-skills
status: draft
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

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Navigate to Settings → Analytics → Skills tab | Skills analytics page loads |
| 2 | Check the 4 summary cards at top | Cards display: "SKILL RUNS", "SKILLS USED", "AGENT & CHAT USES", "SKILL RUN COST" |
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
- Summary cards (Skills tab): "AGENT & CHAT USES"
- Table column header: "AGENT & CHAT USES"
- Chart legend: "Agent & chat uses" (lowercase after bullet)
- Skill detail page: "AGENT & CHAT USES"
- Guide tab: "Agent & Chat Uses"
- Excel export: "Agent & Chat Uses"
- No instances of "In-agent uses" found

**Fail:**
- Any instance of "In-agent uses" found in UI
- Excel export uses old terminology
- Inconsistent naming across different surfaces

## Notes

**Source functional tests:** ELITEA-4208

**Regression rationale:** Critical smoke test for Skills Analytics terminology migration. Verifies complete consistency across 12 UI surfaces (summary cards, table headers, charts, skill detail page, Guide tab, Excel export). High business impact if terminology is inconsistent — users would be confused by mixed naming.

**Selected checkpoints:** All major surfaces where the metric appears — overview cards, table headers, chart legends, detail page, Guide documentation, and data export. Ensures end-to-end terminology consistency.
