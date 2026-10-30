---
id: ELITEA-3831
title: "Verify tooltip content on Skill Activity table headers"
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
| 2 | Scroll to Skill Activity table | Table is visible |
| 3 | Hover over "RUNS" column header (with ⓘ icon) | Tooltip displays: "Times a skill answered by itself during the selected date range: from its Run panel, as a chat participant, or through the API or MCP. Each reply is one run, with its own tokens and cost." |
| 4 | Hover over "AGENT & CHAT USES" column header (with ⓘ icon) | Tooltip displays: "Times a skill was used inside an agent or chat during the selected date range, because it was mentioned in a message or the model loaded it. Counted once per skill per reply for each way it was used. Uses add no tokens or cost here; that cost is on the agent or chat." |
| 5 | Hover over "AGENTS USING" column header (with ⓘ icon) | Tooltip displays: "Different Agents that used this skill. An Agent that runs inside a Pipeline counts as that Pipeline. Chats with only a model are not counted. One agent using it 10 times counts as 1." |
| 6 | Hover over "USERS" column header (with ⓘ icon) | Tooltip displays: "Distinct users who ran this skill or used it in an agent or chat." |
| 7 | Verify ⓘ icons are visible on all 4 headers | All icons present and visible |
| 8 | Verify tooltips appear immediately on hover | Tooltips display without delay |

## Expected Final State

All 4 column headers (RUNS, AGENT & CHAT USES, AGENTS USING, USERS) display ⓘ icons with accurate, helpful tooltips that clarify the difference between runs and uses.

## Pass/Fail Criteria

**Pass:**
- All 4 column headers display ⓘ icon
- Tooltips appear on hover with correct content
- Tooltip text matches specification exactly
- Tooltips are readable and properly formatted
- Tooltips explain the distinction between runs and agent/chat uses
- Cost attribution clearly stated: "Uses add no tokens or cost here; that cost is on the agent or chat"

**Fail:**
- Missing ⓘ icons on any header
- Tooltips don't appear or have incorrect content
- Tooltips are truncated or unreadable
- Old tooltip text referencing "In-agent uses"

## Notes

**Source functional tests:** ELITEA-4209

**Regression rationale:** Critical UX verification. These tooltips clarify the fundamental difference between "runs" (direct skill execution with its own cost) and "agent/chat uses" (skill invoked within an agent/chat, cost attributed to parent). Core to user understanding of Skills Analytics metrics and cost attribution model.

**Selected checkpoints:** All 4 table header tooltips with exact content verification, focusing on the cost attribution explanation which is the primary user confusion point.
