---
id: ELITEA-2702
title: "Tool Selection Persistence After Save"
priority: high
type: functional
module: toolkit/group-tools-within-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, tools, grouping, persistence]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2702: Tool Selection Persistence After Save

**Module:** Toolkit / Group Tools Within Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify tool selections persist correctly after save with the grouped UI structure.

**Coverage:**
- Selection changes in multiple groups are saved
- Exact tools remain selected after reopen (not different tools)
- Counts match after reopen
- No data loss or corruption

## Preconditions

- Logged in to {{base_url}}
- SDK toolkit exists
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an existing toolkit. Note current selection state in each group. | Selection state documented. |
| 2 | Select 2-3 additional tools from **Read** group. | Tools become selected. Count updates. |
| 3 | Select 1-2 tools from **Create & update** group. | Tools become selected. Count updates. |
| 4 | Deselect 1 tool from **Delete** group (if any selected). | Tool deselected. Count updates. |
| 5 | Note final selection state: specific tool names and counts per group. | Final state documented. |
| 6 | Click **Save**. | Save completes successfully. |
| 7 | Close the toolkit and reopen it. | Toolkit reopens. |
| 8 | Verify counts in each group match the saved state. | Counts **match exactly**. |
| 9 | Verify the **specific tools** selected are the same (not different tools with same count). | **Same tools** are selected as before save. |

## Expected Final State

All tool selections persist exactly as saved.

## Pass/Fail Criteria

**Pass:**
- All selections persist after save
- Counts match exactly
- Same specific tools remain selected
- No data loss

**Fail:**
- Selections lost after save
- Counts don't match
- Different tools selected than what was saved
