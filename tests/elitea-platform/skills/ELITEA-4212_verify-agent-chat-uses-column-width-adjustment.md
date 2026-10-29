---
id: ELITEA-4212
title: "Verify Agent & Chat Uses column width adjustment"
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
- Skills analytics page displays table with multiple columns

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/settings/analytics` |
| Tab | Skills |
| Browser widths | 1920px, 1440px, 1280px |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Navigate to Settings → Analytics → Skills | Skills analytics page loads |
| 2 | Observe Skill Activity table column headers at full screen (1920px) | All column headers visible |
| 3 | Check "AGENT & CHAT USES" column header text wrapping | Header text wraps to 2 lines: "AGENT &" on line 1, "CHAT USES" on line 2 |
| 4 | Check "AGENTS USING" column header text wrapping | Header text wraps to 2 lines similarly |
| 5 | Compare "AGENT & CHAT USES" column width to adjacent columns | Column has adequate width, not too narrow or wide |
| 6 | Check that numeric values in the column display fully | All numbers visible without truncation (e.g., "16", "24", "3") |
| 7 | Resize browser window to 1440px width | Table adjusts, remains readable |
| 8 | Check "AGENT & CHAT USES" column at 1440px | Header still wraps appropriately, values visible |
| 9 | Resize browser window to 1280px width | Table adjusts, may show horizontal scroll if needed |
| 10 | Check "AGENT & CHAT USES" column at 1280px | Column maintains readability |
| 11 | Verify table layout is balanced | No columns are disproportionately wide or narrow |

## Expected Final State

"AGENT & CHAT USES" column header wraps consistently with other multi-word headers (e.g., "AGENTS USING"), and the column width accommodates numeric values comfortably without horizontal scrolling at standard screen widths.

## Pass/Fail Criteria

**Pass:**
- "AGENT & CHAT USES" column header wraps to 2 lines
- Header wrapping is consistent with other multi-word headers
- Column width accommodates numeric values without truncation
- Table layout is balanced and readable at 1920px, 1440px, and 1280px
- No unnecessary horizontal scrolling at standard widths

**Fail:**
- Header doesn't wrap or wraps awkwardly
- Column is too narrow, causing value truncation
- Column is disproportionately wide compared to others
- Horizontal scrolling required at standard screen widths
- Inconsistent wrapping compared to other headers
