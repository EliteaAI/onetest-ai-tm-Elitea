---
id: ELITEA-3628
title: "Regression - Run History Panel Not Affected"
priority: high
type: regression
module: per-run-analytics
status: draft
execution_type: manual
tags: [feat:agents, feat:pipelines, issue:6816, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3628: Regression - Run History Panel Not Affected

**Module:** Per-Run Analytics · **Priority:** High · **Type:** Regression

**Objective:** Verify Run History panel functionality is unchanged after Analytics addition to context menu.

## Preconditions

- Logged into {{base_url}}
- Agent with multiple prior runs exists

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to an Agent with prior runs. | Agent page loads. |
| 2 | Locate history icon button in chat area. | Icon visible. |
| 3 | Click history icon. | Run History panel opens. |
| 4 | Verify panel title is "Run History". | Title correct. |
| 5 | Verify table has 3 columns: Date, Version, Duration. | Columns unchanged. |
| 6 | Verify runs are listed with correct data. | Data displayed in each column. |
| 7 | Right-click on a run row. | Context menu appears. |
| 8 | Verify "Restore chat" option is present. | Option visible. |
| 9 | Click "Restore chat" option. | Conversation loads in chat area. |
| 10 | Verify conversation messages restored. | Previous messages displayed. |
| 11 | Re-open Run History panel. | Panel opens. |
| 12 | Click X button to close panel. | Panel closes cleanly. |
| 13 | Open and close panel 3 times rapidly. | No errors or glitches. |

## Automation Notes

- Test both Agent and Pipeline Run History
- Check for console errors during operations
- Verify chat area state before/after restore

## Pass/Fail Criteria

**Pass:** Run History works as before, Restore chat functional, panel open/close stable.
**Fail:** Any existing functionality broken or changed.
