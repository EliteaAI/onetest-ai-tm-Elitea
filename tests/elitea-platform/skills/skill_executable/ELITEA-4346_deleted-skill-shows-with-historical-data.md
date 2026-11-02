---
id: ELITEA-4346
title: "Verify deleted skill still appears in Analytics with historical data and last known name"
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
- Test skill has been executed multiple times (standalone and in-agent)
- User has permission to delete skills

## Test Data

| Field | Value |
|-------|-------|
| Test Skill | skill-to-be-deleted |
| Standalone Runs | 10 runs with cost $0.05 |
| In-Agent Uses | 15 uses |
| Analytics URL | `{{base_url}}/settings/analytics?tab=skills` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute test skill standalone 10 times | 10 standalone runs completed, cost $0.05 recorded |
| 2 | Execute test skill in-agent 15 times | 15 in-agent uses recorded |
| 3 | Navigate to Settings → Analytics → Skills tab | Skills analytics page loads |
| 4 | Search for test skill and verify it appears with Runs=10, Agent & Chat Uses=15, Cost=$0.05 | Test skill found with correct metrics |
| 5 | Record the skill name displayed: "skill-to-be-deleted" | Skill name recorded |
| 6 | Navigate to Skills page and delete the test skill | Skill deleted successfully (confirm deletion dialog) |
| 7 | Verify skill no longer appears in Skills list or catalog | Skill removed from active skills list |
| 8 | Navigate back to Settings → Analytics → Skills tab | Skills analytics page loads |
| 9 | Search for "skill-to-be-deleted" in Skill Activity table | Deleted skill still appears in table |
| 10 | Verify skill displays last known name: "skill-to-be-deleted" | Name displayed correctly (last known name) |
| 11 | Verify skill has a "deleted" marker or visual indicator (icon, label, strikethrough, etc.) | "Deleted" marker visible (e.g., grayed out, icon, or "(deleted)" suffix) |
| 12 | Verify historical metrics are still displayed: Runs=10, Agent & Chat Uses=15, Cost=$0.05 | All historical metrics intact |
| 13 | Click on deleted skill name to open detail page | Skill detail page opens |
| 14 | Verify detail page shows full historical data: KPIs, trend chart, breakdowns | All historical data displayed correctly |
| 15 | Verify "deleted" indicator appears on detail page as well | "Deleted" marker visible on detail page |

## Expected Final State

- Deleted skill still appears in Skills analytics with historical data
- Last known name displayed correctly
- "Deleted" visual marker present
- All metrics, trends, and breakdowns intact
- No data loss after skill deletion

## Pass/Fail Criteria

**Pass:**
- Deleted skill appears in Analytics Skills list
- Last known name "skill-to-be-deleted" displayed
- "Deleted" marker or indicator visible (icon, label, grayed out, etc.)
- Historical metrics intact: Runs=10, Agent & Chat Uses=15, Cost=$0.05
- Skill detail page accessible and shows full historical data
- No errors or data corruption

**Fail:**
- Deleted skill missing from Analytics
- Skill name changed or shows as null/empty
- No "deleted" indicator (confusing with active skills)
- Historical metrics lost or zeroed out
- Skill detail page inaccessible or errors
- Data corruption after deletion
