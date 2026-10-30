---
id: ELITEA-3835
title: "Verify search functionality with updated terminology"
priority: medium
type: ui
module: analytics-skills
status: draft
execution_type: manual
tags: [feat:analytics, feat:skills, r-2.0.8, nfr:usability]
requirements: [EliteaAI/elitea_issues#7272]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Multiple skills exist with different usage patterns

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/settings/analytics` |
| Tab | Skills |
| Search terms | Partial skill names, full skill names |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Navigate to Settings → Analytics → Skills | Skills analytics page loads |
| 2 | Locate the skill count text above Skill Activity table | Displays: "N skills" (e.g., "55 skills") |
| 3 | Hover over the info icon (ⓘ) next to "N skills" text | Tooltip displays: "Skills in the table below that were run or used during the selected date range. Follows the search." |
| 4 | Locate "Search by skill name" input box | Search box is visible above or within the table |
| 5 | Type a partial skill name (e.g., "status") | Table filters to show only matching skills |
| 6 | Observe "N skills" count update | Count updates to reflect filtered results (e.g., "1 skill" or "3 skills") |
| 7 | Check that filtered skills display "AGENT & CHAT USES" column correctly | Column header and values display correctly for filtered results |
| 8 | Check that all other columns display correctly for filtered skills | RUNS, AGENTS USING, AVG LATENCY, TOKENS, COST, LAST USED all display correctly |
| 9 | Clear search by deleting text or clicking X | All skills reappear in table |
| 10 | Verify "N skills" count returns to original total | Count shows all skills again |

## Expected Final State

Search functionality works correctly with the updated "Agent & Chat Uses" terminology, and the skill count tooltip accurately explains that it follows the search filter.

## Pass/Fail Criteria

**Pass:**
- Search functionality filters skills correctly
- "N skills" count updates based on search results
- "N skills" tooltip uses updated terminology: "run or used"
- Filtered results maintain correct column headers and values
- "AGENT & CHAT USES" column displays correctly for filtered results
- Empty search shows all skills
- All columns display accurately during filtering

**Fail:**
- Search doesn't filter correctly
- Skill count doesn't update
- Tooltip references old "In-agent uses" terminology
- Filtered results show incorrect data
- Search breaks column display

## Notes

**Source functional tests:** ELITEA-4214

**Regression rationale:** Confirms search/filter functionality preserves correct column display and the skill count tooltip references updated terminology. Secondary but useful coverage that ensures interactive filtering doesn't break the new terminology or data display.

**Selected checkpoints:** Skill count tooltip content ("run or used" terminology), search filtering behavior, and column display accuracy during filtering, with focus on "AGENT & CHAT USES" column.
