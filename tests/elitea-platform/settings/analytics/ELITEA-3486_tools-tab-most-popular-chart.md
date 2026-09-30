---
id: ELITEA-3486
title: "Tools Tab Most Popular Tools Chart"
priority: high
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3486: Tools Tab Most Popular Tools Chart

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify Most Popular Tools chart displays top tools by usage count.

## Preconditions

- Logged into {{base_url}}
- Project has tool execution history
- Navigate to Settings → Analytics → Tools

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click on "Tools" tab. | Tab loads with chart and tool details table. |
| 2 | Locate "Most Popular Tools" chart. | Bar chart visible with subtitle "Top X by usage". |
| 3 | Verify bars represent different tools. | Each bar corresponds to a unique tool. |
| 4 | Hover over bars. | Tooltip shows tool name and call count. |
| 5 | Verify X-axis shows tool names. | Tool names like "pyodide_sandbox", "create_file" visible. |

## Pass/Fail Criteria

**Pass:** Chart shows most used tools ranked by call count.
**Fail:** Chart empty when tools were used, or incorrect ranking.
