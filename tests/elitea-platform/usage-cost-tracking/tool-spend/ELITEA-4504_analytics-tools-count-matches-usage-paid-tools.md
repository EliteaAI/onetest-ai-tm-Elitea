---
id: ELITEA-4504
title: "Analytics Tools tab call count matches Paid Tools spend on Usage page"
priority: high
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6980]
---
# ELITEA-4504: Analytics Tools tab call count matches Paid Tools spend on Usage page

**Module:** Usage Cost Tracking · **Priority:** High · **Type:** Functional

**Objective:** Confirm that the call count shown for the paid tool in Settings → Analytics → Tools (Tool Details table) is consistent with the call count shown in Settings → Usage → Paid Tools, for the same date range/project.

**Coverage:**
- Call counts consistent between Analytics and Usage
- Error calls reflected in Analytics without affecting the Paid Tools $ spend figure

## Preconditions

- Project has the paid-tool module enabled

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/analytics`, `{{base_url}}/app/settings/usage` |
| Example calls to trigger | 5 paid-tool calls |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger a known number of paid-tool calls (e.g. 5). | Calls succeed. |
| 2 | Open Settings → Analytics → Tools tab, filter/select a date range covering the test window. | "CALLS" value for the tool (e.g. `web_search`) is noted. |
| 3 | Open Settings → Usage, note the call count in the Paid Tools section for the same tool/feature and overlapping period. | Call count noted. |
| 4 | Compare the two counts. | Counts are consistent (no unexplained discrepancy). |
| 5 | If any error calls occurred, check the Analytics "ERRORS" column. | Errors are reflected in Analytics without affecting the Paid Tools $ spend figure for failed/denied attempts. |

## Expected Final State

Tool-call telemetry in Analytics and spend tracking in Usage remain consistent with each other for the same tool and time window.

## Pass/Fail Criteria

**Pass:**
- Call counts are consistent between Analytics and Usage
- Error calls do not affect the $ spend figure

**Fail:**
- Call counts diverge without explanation, or error calls incorrectly affect $ spend
