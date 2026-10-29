---
id: ELITEA-4211
title: "Verify summary card tooltips on Skills tab"
priority: high
type: ui
module: analytics-skills
status: ready
execution_type: manual
tags: [feat:analytics, feat:skills, r-2.0.8, nfr:usability]
requirements: [EliteaAI/elitea_issues#7272]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Skills analytics page is accessible

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/settings/analytics` |
| Tab | Skills |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Navigate to Settings → Analytics → Skills | Skills analytics page loads |
| 2 | Locate the 4 summary cards at the top | Cards visible: SKILL RUNS, SKILLS USED, AGENT & CHAT USES, SKILL RUN COST |
| 3 | Hover over "SKILL RUNS" card info icon (ⓘ) | Tooltip displays: "Times a skill answered by itself during the selected date range: from its Run panel, as a chat participant, or through the API or MCP. Each reply is one run, with its own tokens and cost." |
| 4 | Hover over "SKILLS USED" card info icon (ⓘ) | Tooltip displays: "Number of different skills that were run or used in an agent or chat during the selected date range. Each skill counts once, however many times it was used." |
| 5 | Hover over "AGENT & CHAT USES" card info icon (ⓘ) | Tooltip displays: "Times a skill was used inside an agent or chat during the selected date range, because it was mentioned in a message or the model loaded it. Counted once per skill per reply for each way it was used. Uses add no tokens or cost here; that cost is on the agent or chat." |
| 6 | Hover over "SKILL RUN COST" card info icon (ⓘ) | Tooltip displays: "Total estimated cost of all skill runs during the selected date range. Each model call is priced by the model it used. Uses inside agents or chats are not included; that cost is on the agent or chat." |
| 7 | Verify all tooltips are properly formatted and readable | Text is clear, no truncation or overflow |
| 8 | Verify tooltips disappear when cursor moves away | Tooltips hide properly |

## Expected Final State

All 4 summary cards have functional info icons with tooltips that clearly explain each metric and differentiate between skill runs and agent/chat uses.

## Pass/Fail Criteria

**Pass:**
- All 4 summary cards have visible info icons (ⓘ)
- Tooltips display on hover
- Tooltip content matches specification exactly
- Tooltips clarify the difference between runs and uses
- Tooltips explain cost attribution correctly
- All tooltips are readable and properly formatted

**Fail:**
- Missing info icons on any card
- Tooltips don't appear or have incorrect content
- Tooltips reference old "In-agent uses" terminology
- Tooltips don't explain cost attribution
- Tooltips are truncated or have formatting issues
