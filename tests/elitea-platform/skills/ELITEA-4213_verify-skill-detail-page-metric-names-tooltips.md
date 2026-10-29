---
id: ELITEA-4213
title: "Verify skill detail page metric names and tooltips"
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
| 8 | Hover over Versions section info icon (if present) | Tooltip displays: "Runs and uses per skill version. Unknown version means the version was not recorded." |
| 9 | Scroll to "Used by Agents" section | Section visible with list of agents |
| 10 | Hover over "Used by Agents" info icon (if present) | Tooltip displays: "Agents that used this skill, by number of uses. An Agent that runs inside a Pipeline is listed as that Pipeline." |
| 11 | Scroll to "Load vs Mention" section | Section visible with activation breakdown |
| 12 | Hover over "Load vs Mention" info icon (if present) | Tooltip displays: "How this skill was used: loaded on demand (load_skill) or mentioned in the message." |
| 13 | Verify no references to "In-agent uses" anywhere on page | All text uses "Agent & Chat Uses" terminology |

## Expected Final State

Skill detail page consistently uses "Agent & Chat Uses" terminology across all sections, with accurate tooltips that clarify each metric and explain the difference between runs and uses.

## Pass/Fail Criteria

**Pass:**
- All metric names use "Agent & Chat Uses" terminology
- All summary cards have info icons with correct tooltips
- Section headers use updated terminology
- Section tooltips (if present) are accurate
- No references to old "In-agent uses" terminology
- All tooltips are clear and match specification

**Fail:**
- Any reference to "In-agent uses" found
- Missing or incorrect tooltips
- Inconsistent terminology across sections
- Tooltips don't match specification
