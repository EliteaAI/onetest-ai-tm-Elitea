---
id: ELITEA-2690
title: "Selected/Total Counts in Group Headers Include Filtered-Out Tools"
priority: critical
type: functional
module: toolkits-credentials/group-tools-within-toolkit
status: ready
execution_type: manual
tags: [feat:toolkits, tools, search, counts]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2690: Selected/Total Counts in Group Headers Include Filtered-Out Tools

**Module:** Toolkits Credentials / Group Tools Within Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that group header counts always reflect the entire group, not just the currently visible filtered subset.

**Coverage:**
- Group counts always reflect total group composition
- Counts do not change based on search filter (except when tools are selected/deselected)
- Selected count updates when tools are toggled, regardless of filter state
- Total count remains constant (represents all tools in group)

## Preconditions

- Logged in to {{base_url}}
- User has access to ELITEA platform
- SDK toolkit where Read group has 20+ total tools exists
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a toolkit where Read group has 26 total tools, with 10 selected. | Toolkit opens, Read group is visible. |
| 2 | Verify Read group header count. | Read group header shows **"10 / 26"**. |
| 3 | Type **"file"** in search field (filters to show only ~4 Read tools matching "file"). | Only ~4 Read tools are visible. |
| 4 | Verify Read group header count while filter is active. | Read group header still shows **"10 / 26"** (NOT "2 / 4" or similar filtered count). |
| 5 | Select one more visible Read tool (one of the "file" tools). | Tool becomes selected. |
| 6 | Verify Read group header count after selection. | Count updates to **"11 / 26"**. |
| 7 | Clear the search field. | All Read tools become visible again. |
| 8 | Verify count remains accurate. | Count remains **"11 / 26"**. |
| 9 | Verify the newly selected tool is still selected. | Newly selected tool shows as selected. |
| 10 | Type a different search term that shows different Read tools. | Different subset of Read tools is visible. |
| 11 | Verify count still shows correct total. | Count still shows **"11 / 26"**. |

## Expected Final State

Group counts accurately reflect total composition regardless of search filter state.

## Pass/Fail Criteria

**Pass:**
- Group counts always reflect total group composition (not filtered subset)
- Counts do not change based on search filter unless selections change
- Selected count updates when tools are toggled
- Total count remains constant

**Fail:**
- Counts change to reflect only visible/filtered tools
- Selected count does not update when toggling visible tools
- Total count changes based on filter
