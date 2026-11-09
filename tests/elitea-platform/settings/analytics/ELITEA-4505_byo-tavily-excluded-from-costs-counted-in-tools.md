---
id: ELITEA-4505
title: "BYO Tavily toolkit calls and costs are excluded from Usage and Costs tabs but counted in Tools tab"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6980]
---
# ELITEA-4505: BYO Tavily toolkit calls and costs are excluded from Usage and Costs tabs but counted in Tools tab

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Confirm that calls made through a Tavily (or other paid-tool) toolkit configured with the user's own credential are excluded from the Settings → Usage "Paid Tools" figures and from Settings → Analytics → Costs tab, while still appearing as call activity in Settings → Analytics → Tools tab.

**Coverage:**
- Paid Tools and Costs figures unchanged by BYO calls
- Tools tab call count correctly increases for BYO calls

## Preconditions

- A toolkit instance for the paid tool (e.g. Tavily) is configured with the user's own (BYO) credential, distinct from the platform-shared one

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/usage`, `{{base_url}}/app/settings/analytics` |
| Example calls to trigger | 3 calls using BYO-credential toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Record baseline: Settings → Usage → Paid Tools line for the feature; Settings → Analytics → Costs tab totals; Settings → Analytics → Tools tab call count for the tool. | Baseline values recorded. |
| 2 | Trigger a known number of calls (e.g. 3) using the BYO-credential toolkit. | Calls succeed. |
| 3 | Refresh Settings → Usage. | Paid Tools $ spent and call count for the feature are unchanged (BYO calls not added). |
| 4 | Refresh Settings → Analytics → Costs tab. | Total/estimated cost figures are unchanged (no cost attributed to BYO calls). |
| 5 | Refresh Settings → Analytics → Tools tab. | Call count for the tool increased by the expected number (BYO calls show up as tool activity), errors/latency columns update normally. |

## Expected Final State

BYO-credential usage is excluded from spend/cost tracking (Usage, Costs) but included in generic tool-call activity tracking (Analytics → Tools).

## Pass/Fail Criteria

**Pass:**
- Paid Tools and Costs figures unchanged by BYO calls
- Tools tab call count correctly increases for BYO calls

**Fail:**
- BYO calls incorrectly affect Paid Tools or Costs figures, or fail to appear in Tools tab activity
