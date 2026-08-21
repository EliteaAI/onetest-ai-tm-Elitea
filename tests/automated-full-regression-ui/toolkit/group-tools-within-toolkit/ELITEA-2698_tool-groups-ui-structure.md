---
id: ELITEA-2698
title: "Tool Groups UI Structure and Sorting"
priority: critical
type: functional
module: toolkit/group-tools-within-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, tools, grouping, ui, sorting]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2698: Tool Groups UI Structure and Sorting

**Module:** Toolkit / Group Tools Within Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify tool groups render in correct order with proper UI elements (badges, tooltips, counts) and tools are alphabetically sorted within each group.

**Coverage:**
- Groups appear in fixed order: Read → Create & update → Delete → Execute
- Each group has correct badge, info icon with tooltip, and selected/total count
- Empty groups are hidden
- Tools alphabetically sorted within each group

## Preconditions

- Logged in to {{base_url}}
- SDK toolkit with tools across multiple groups exists (e.g., GitHub toolkit)
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits page and open an SDK toolkit with tools in all four groups (e.g., GitHub). | Toolkit configuration page opens. |
| 2 | Scroll to Tools section and verify group order from top to bottom. | Groups appear in exact order: **Read** → **Create & update** → **Delete** → **Execute**. |
| 3 | Verify **Read** group header elements. | Label "Read", badge "Read-only", ⓘ icon present, count format "X / Y". |
| 4 | Verify **Create & update** group header elements. | Label "Create & update", badge "Changes data", ⓘ icon present, count displayed. |
| 5 | Verify **Delete** group header elements. | Label "Delete", badge "Destructive", ⓘ icon present, count displayed. |
| 6 | Verify **Execute** group header elements. | Label "Execute", badge "Unrestricted", ⓘ icon present, count displayed. |
| 7 | Hover over ⓘ icon next to **Read** group. | Tooltip: "Returns data. Nothing is created, changed or destroyed." |
| 8 | Hover over ⓘ icon next to **Create & update** group. | Tooltip: "Creates or modifies data in the target system." |
| 9 | Hover over ⓘ icon next to **Delete** group. | Tooltip: "Destroys data. Not reversible from Elitea." |
| 10 | Hover over ⓘ icon next to **Execute** group. | Tooltip: "Runs a caller-supplied query, script, pipeline or raw API call. Effect is not bounded by the tool." |
| 11 | In each group, verify tools are sorted alphabetically (A-Z). | All tools within each group are in **strict alphabetical order**. |
| 12 | Open a toolkit with fewer groups (e.g., Jira — may not have Delete/Execute). | Toolkit opens. |
| 13 | Verify only non-empty groups are displayed. | Empty groups are **hidden** — no headers or placeholders shown. |

## Expected Final State

Tool groups display with correct UI structure, tooltips, and alphabetical sorting.

## Pass/Fail Criteria

**Pass:**
- Groups in correct fixed order
- Correct badges: Read-only, Changes data, Destructive, Unrestricted
- Info icons show correct tooltip text
- Selected/total counts displayed
- Empty groups hidden
- Tools alphabetically sorted within each group

**Fail:**
- Wrong group order
- Missing or incorrect badges/tooltips
- Empty groups displayed
- Tools not sorted alphabetically
