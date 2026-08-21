---
id: ELITEA-2692
title: "Tool Selection Persistence After Save with Grouped UI"
priority: high
type: functional
module: toolkits-credentials/group-tools-within-toolkit
status: ready
execution_type: manual
tags: [feat:toolkits, tools, grouping, persistence, regression]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
  - ELITEA-2539
---
# ELITEA-2692: Tool Selection Persistence After Save with Grouped UI

**Module:** Toolkits Credentials / Group Tools Within Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Re-validate that selected tools persist correctly after saving with the new grouped UI structure. (Re-validation of ELITEA-2539)

**Coverage:**
- All tool selections persist after save
- Group counts match expected values after reopen
- Specific tools remain selected (not randomly different tools)
- No data loss or corruption in tool selections

## Preconditions

- Logged in to {{base_url}}
- User has access to ELITEA platform
- SDK toolkit exists
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an existing toolkit and note the current tool selections in each group. | Current selection state is documented. |
| 2 | Make the following selection changes: Select 3 additional tools from Read group. | 3 additional Read tools are selected. |
| 3 | Select 2 additional tools from Create & update group. | 2 additional Create & update tools are selected. |
| 4 | Deselect 1 tool from Delete group. | 1 Delete tool is deselected. |
| 5 | Select 1 tool from Execute group. | 1 Execute tool is selected. |
| 6 | Note the final selection state for each group (Read: X / Y, Create & update: A / B, Delete: C / D, Execute: E / F). | Final selection state is documented. |
| 7 | Click **Save** button. | Save completes **successfully**. |
| 8 | Close the toolkit and reopen the same toolkit. | Toolkit reopens. |
| 9 | Navigate to Tools section and verify all selections match the saved state. | Read group has X tools selected, Create & update has A, Delete has C, Execute has E. Counts **match exactly**. |
| 10 | Verify the specific tools selected are the correct ones (not different tools with same count). | **Same specific tools** are selected as before save. |

## Expected Final State

All tool selections persist correctly after save, with exact tools and counts preserved.

## Pass/Fail Criteria

**Pass:**
- All tool selections persist after save
- Group counts match expected values after reopen
- Specific tools remain selected (not randomly different tools)
- No data loss or corruption in tool selections

**Fail:**
- Any tool selections are lost after save
- Group counts do not match
- Different tools are selected than what was saved
- Data corruption occurs in tool selections
