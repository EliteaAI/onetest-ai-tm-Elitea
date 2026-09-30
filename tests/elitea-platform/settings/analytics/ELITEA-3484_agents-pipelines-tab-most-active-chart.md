---
id: ELITEA-3484
title: "Agents & Pipelines Tab Most Active Chart"
priority: high
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3484: Agents & Pipelines Tab Most Active Chart

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify Most Active Agents & Pipelines chart displays top entities by run count.

## Preconditions

- Logged into {{base_url}}
- Project has agent/pipeline execution history
- Navigate to Settings → Analytics → Agents & Pipelines

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click on "Agents & Pipelines" tab. | Tab loads with chart and activity table. |
| 2 | Locate "Most Active Agents & Pipelines" chart. | Bar chart visible with subtitle "Top 2 by runs" (or similar). |
| 3 | Verify bars show agent/pipeline names on hover. | Tooltip displays entity name and run count (e.g., "CodeExecutor (scheduled): Runs: 9"). |
| 4 | Verify X-axis labels show entity names. | Entity names displayed (may be rotated for long names). |
| 5 | Verify Y-axis shows run count. | Numeric scale starting at 0. |

## Pass/Fail Criteria

**Pass:** Chart shows most active entities with correct run counts.
**Fail:** Chart empty when data exists, or tooltips not working.
