---
id: ELITEA-3834
title: "Verify skill detail page metric names and tooltips"
priority: high
type: ui
module: analytics-skills
status: draft
execution_type: manual
tags: [feat:analytics, feat:skills, r-2.0.8, nfr:usability]
requirements: [EliteaAI/elitea_issues#7272]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least one skill with usage data exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/settings/analytics` |
| Tab | Skills |
| Skill | Any skill with runs and agent/chat uses |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Navigate to Settings → Analytics → Skills | Skills analytics page loads |
| 2 | Click on any skill name in the Skill Activity table | Skill detail page opens |
| 3 | Check summary cards at top of page | Cards display: "RUNS", "AGENT & CHAT USES", "AGENTS USING", "UNIQUE USERS" |
| 4 | Hover over "RUNS" card info icon (ⓘ) | Tooltip displays: "Runs of this skill on its own, as a chat participant, or through the API or MCP during the selected date range." |
| 5 | Hover over "AGENT & CHAT USES" card info icon (ⓘ) | Tooltip displays: "Times this skill was used inside an agent or chat during the selected date range, mentioned in a message or loaded by the model." |
| 6 | Hover over "AGENTS USING" card info icon (ⓘ) | Tooltip displays: "Different Agents that used this skill. An Agent that runs inside a Pipeline counts as that Pipeline. Chats with only a model are not counted. One agent using it 10 times counts as 1." |
| 7 | Scroll down to Versions section | Section header displays: "Runs · Agent & Chat Uses" |
| 8 | Verify no references to "In-agent uses" anywhere on page | All text uses "Agent & Chat Uses" terminology |

## Expected Final State

Skill detail page consistently uses "Agent & Chat Uses" terminology across all sections, with accurate tooltips that clarify each metric and explain the difference between runs and uses.

## Pass/Fail Criteria

**Pass:**
- All metric names use "Agent & Chat Uses" terminology
- All summary cards have info icons with correct tooltips
- "Versions" section header uses updated terminology: "Runs · Agent & Chat Uses"
- No references to old "In-agent uses" terminology
- All tooltips are clear and match specification

**Fail:**
- Any reference to "In-agent uses" found
- Missing or incorrect tooltips
- Inconsistent terminology across sections
- Tooltips don't match specification

## Notes

**Source functional tests:** ELITEA-4213

**Regression rationale:** Important drill-down UX verification. Ensures terminology and explanations are consistent on skill detail pages, which users visit to investigate specific skill performance. The "Versions" section header is particularly important as it shows per-version breakdown of runs and uses.

**Selected checkpoints:** Summary card labels and tooltips on detail page, plus "Versions" section header. Focuses on the most visible and frequently accessed drill-down view.
