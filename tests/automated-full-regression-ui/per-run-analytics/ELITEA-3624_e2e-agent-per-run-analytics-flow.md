---
id: ELITEA-3624
title: "E2E Agent Per-Run Analytics Flow"
priority: critical
type: e2e
module: per-run-analytics
status: draft
execution_type: automated
tags: [feat:analytics, feat:agents, eng:frontend, issue:6816, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3624: E2E Agent Per-Run Analytics Flow

**Module:** Per-Run Analytics · **Priority:** Critical · **Type:** E2E Regression

**Objective:** End-to-end verification of Per-Run Analytics for Agents: navigation, UI structure, data display, and export.

## Preconditions

- Logged into {{base_url}}
- Agent with multiple prior runs exists (including runs with tools)
- Test data: Agent "Regression Test Agent" with runs from different versions

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents page. | Agents list loads. |
| 2 | Open "Regression Test Agent". | Agent detail page opens. |
| 3 | Click history icon to open Run History panel. | Panel opens with run list. |
| 4 | Right-click on most recent run row. | Context menu appears. |
| 5 | Verify "Analytics" option present after "Restore chat". | Option visible in correct position. |
| 6 | Click "Analytics" option. | Per-Run Analytics page opens. |
| 7 | Verify breadcrumb: `Agents / [Name] / Run History / Analytics`. | Breadcrumb correct. |
| 8 | Verify header format: "Run: [date] · Version: [version]". | Header displays correctly. |
| 9 | Verify 4 tabs: Costs (active), Tokens, Tools, Health. | Tabs present in order. |
| 10 | **Costs Tab:** Verify info banner displayed. | Banner with disclaimer visible. |
| 11 | Verify 5 cost cards with values (6 decimal max). | All cards present with proper precision. |
| 12 | Verify Cost by User and Cost by Model tables. | Tables displayed with data. |
| 13 | Click "Tokens" tab. | Tab activates. |
| 14 | Verify 5 token cards with K/M suffix formatting. | All cards present with proper formatting. |
| 15 | Verify Usage by User and Usage by Model tables. | Tables displayed. |
| 16 | Click "Tools" tab. | Tab activates. |
| 17 | Verify Tool Details table with 5 columns. | TOOL, CALLS, USERS, AVG LATENCY, ERRORS columns. |
| 18 | Verify latency format (Xs or Yms). | Proper time format. |
| 19 | Click "Health" tab. | Tab activates. |
| 20 | Verify Event Type table with 5 columns and status indicators. | Green/red dots based on error rate. |
| 21 | Click Export button. | Download initiates. |
| 22 | Verify .xlsx file downloads. | File extension correct. |
| 23 | Open Excel and verify 4 sheets: Costs, Tokens, Tools, Health. | All sheets present with data. |
| 24 | Click breadcrumb "Agents" segment. | Navigates to Agents list. |

## Automation Notes

- Use data-testid selectors where available
- Store UI values before export for comparison
- Handle file download and Excel parsing
- Use explicit waits for tab content loading

## Pass/Fail Criteria

**Pass:** Complete flow works: navigation → all tabs display correctly → export succeeds with matching data.
**Fail:** Any navigation failure, missing UI elements, or data mismatch.
