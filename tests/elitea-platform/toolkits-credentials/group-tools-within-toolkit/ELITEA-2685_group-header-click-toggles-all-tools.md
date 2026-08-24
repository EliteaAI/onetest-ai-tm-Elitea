---
id: ELITEA-2685
title: "Group Header Click Toggles Selection for All Tools in That Group"
priority: critical
type: functional
module: toolkits-credentials/group-tools-within-toolkit
status: ready
execution_type: manual
tags: [feat:toolkits, tools, grouping, selection]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2685: Group Header Click Toggles Selection for All Tools in That Group

**Module:** Toolkits Credentials / Group Tools Within Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify clicking a group header checkbox/control selects or deselects all tools within that group without affecting other groups.

**Coverage:**
- Group header checkbox selects/deselects all tools in the group
- Other groups remain unaffected
- Selected/total counts update correctly

## Preconditions

- Logged in to {{base_url}}
- User has access to ELITEA platform
- SDK toolkit with tools in multiple groups exists
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a toolkit configuration with tools in the Read group (some selected, some not). Note the initial selected/total count for Read group and the state of tools in other groups. | Toolkit opens. Read group shows partial selection. Other groups have their own selection states. |
| 2 | Click the Read group header checkbox/control. | All tools in the Read group become **selected**. Selected/total count updates (e.g., "26 / 26"). |
| 3 | Verify tools in Create & update, Delete, and Execute groups. | Tools in other groups remain **unchanged** from their initial state. |
| 4 | Click the Read group header checkbox/control again. | All tools in the Read group become **deselected**. Selected/total count shows "0 / 26". |
| 5 | Verify tools in other groups again. | Tools in Create & update, Delete, and Execute groups remain **unchanged**. |
| 6 | Click the Create & update group header checkbox/control. | All tools in Create & update group become **selected**. Count updates accordingly. |
| 7 | Click the Create & update group header checkbox/control again. | All tools in Create & update group become **deselected**. Count shows "0 / N". |
| 8 | Repeat toggle test for Delete group header. | Delete group toggles all its tools on click, count updates, other groups unaffected. |
| 9 | Repeat toggle test for Execute group header. | Execute group toggles all its tools on click, count updates, other groups unaffected. |

## Expected Final State

All groups correctly toggle their tools independently, with accurate count updates.

## Pass/Fail Criteria

**Pass:**
- Clicking group header checkbox selects all tools in that group
- Clicking again deselects all tools in that group
- Tools in other groups remain unchanged during toggle operations
- Selected/total counts update correctly after each toggle

**Fail:**
- Group header click does not select/deselect all tools in the group
- Clicking group header affects tools in other groups
- Selected/total counts do not update correctly
- Toggle behavior is inconsistent across groups
