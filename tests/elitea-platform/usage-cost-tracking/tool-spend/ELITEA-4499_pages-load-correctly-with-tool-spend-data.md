---
id: ELITEA-4499
title: "Default Modules, Usage, and Analytics pages load correctly with Tool Spend data present"
priority: critical
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6980]
---
# ELITEA-4499: Default Modules, Usage, and Analytics pages load correctly with Tool Spend data present

**Module:** Usage Cost Tracking · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm none of the pages touched by this framework (module toggles, Usage page, Analytics Tools/Costs tabs) fail to load, error out, or show a broken layout once paid-tool usage exists in the project.

**Coverage:**
- Default Modules table renders with the paid-tool module row
- Usage page loads across zero/under-limit/at-limit usage states
- Analytics → Tools tab shows the paid tool without errors
- Analytics → Costs tab unaffected by tool-cost data
- Behavior holds for both Team and Personal projects

## Preconditions

- A Team project and a Personal project each have recorded paid-tool usage at varying levels (zero, under limit, at/over limit)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/project-general`, `{{base_url}}/app/settings/usage`, `{{base_url}}/app/settings/analytics` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → General for a Team project. | Default Modules table renders without errors, including the Web Search/paid-tool module row with Chats/Agents toggles. |
| 2 | Navigate to Settings → Usage for a project with zero paid-tool usage. | Page loads fully including the "Paid Tools" section. |
| 3 | Navigate to Settings → Usage for a project with usage under the limit. | Page loads fully, Paid Tools section reflects current usage. |
| 4 | Navigate to Settings → Usage for a project with usage at/over the limit. | Page loads fully, Paid Tools section reflects limit-reached state. |
| 5 | Navigate to Settings → Analytics → Tools tab. | The paid tool (e.g. `web_search`) appears in "Most Popular Tools" and "Tool Details" without errors. |
| 6 | Navigate to Settings → Analytics → Costs tab. | Existing LLM cost breakdown renders correctly, no errors from presence of tool-cost data. |
| 7 | Repeat steps 1–6 for a Personal project. | Same results hold for the Personal project. |

## Expected Final State

All pages touched by the Tool Spend framework load without errors across both project types and all usage states.

## Pass/Fail Criteria

**Pass:**
- All pages load without error in every usage state, for both Team and Personal projects

**Fail:**
- Any page fails to load, errors out, or shows a broken layout in any tested state
