---
id: ELITEA-2699
title: "Group Header Toggle Selects/Deselects All Tools in Group"
priority: critical
type: functional
module: toolkit/group-tools-within-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, tools, grouping, selection]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2699: Group Header Toggle Selects/Deselects All Tools in Group

**Module:** Toolkit / Group Tools Within Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify clicking a group header checkbox toggles selection for all tools in that group without affecting other groups.

**Coverage:**
- Group header click selects all tools in group
- Second click deselects all tools in group
- Other groups remain unaffected
- Counts update correctly

## Preconditions

- Logged in to {{base_url}}
- SDK toolkit with tools in multiple groups exists
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a toolkit configuration with tools in multiple groups. Note initial selection states. | Toolkit opens with current selections visible. |
| 2 | Click the **Read** group header checkbox. | All tools in Read group become **selected**. Count updates to "N / N". |
| 3 | Verify other groups (Create & update, Delete, Execute). | Other groups' selections remain **unchanged**. |
| 4 | Click the **Read** group header checkbox again. | All tools in Read group become **deselected**. Count shows "0 / N". |
| 5 | Verify other groups again. | Other groups' selections still **unchanged**. |
| 6 | Click the **Create & update** group header checkbox. | All Create & update tools become **selected**. Count updates. |
| 7 | Click it again. | All Create & update tools become **deselected**. |
| 8 | Repeat for **Delete** and **Execute** groups. | Each group toggles independently, counts update correctly. |

## Expected Final State

All group header toggles work independently with correct count updates.

## Pass/Fail Criteria

**Pass:**
- Group header click selects all tools in that group
- Second click deselects all tools
- Other groups unaffected
- Counts update correctly after each toggle

**Fail:**
- Toggle does not select/deselect all tools
- Toggle affects other groups
- Counts do not update
