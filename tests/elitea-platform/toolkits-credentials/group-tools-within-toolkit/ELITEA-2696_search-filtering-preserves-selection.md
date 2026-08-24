---
id: ELITEA-2696
title: "Search Filtering Does Not Change Tool Selection State"
priority: critical
type: functional
module: toolkits-credentials/group-tools-within-toolkit
status: ready
execution_type: manual
tags: [feat:toolkits, tools, search, selection]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2696: Search Filtering Does Not Change Tool Selection State

**Module:** Toolkits Credentials / Group Tools Within Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that filtering tools via search is purely visual and never modifies the selected_tools array.

**Coverage:**
- Search filtering is visual only
- Hidden tools retain their selection state
- Changes made during filter are applied correctly
- Clearing search restores full view with correct selections
- Save persists all selection changes correctly

## Preconditions

- Logged in to {{base_url}}
- User has access to ELITEA platform
- SDK toolkit with tools selected across multiple groups exists
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a toolkit with tools selected across multiple groups. Note the current selection state (e.g., 8 tools selected total across Read, Create & update, Delete groups). | Selection state is recorded. |
| 2 | Note which specific tools are selected in each group. | Specific selected tools are documented. |
| 3 | Type **"delete"** in search field to filter to only Delete group tools. | Only Delete group tools are visible. Read, Create & update, Execute groups are hidden. |
| 4 | Verify the selection count indicator (if shown) still reflects all selected tools. | Count indicator shows **total selected tools** (e.g., 8), not just visible ones. |
| 5 | Select one additional visible Delete tool while filter is active. | Tool becomes selected. |
| 6 | Deselect one visible Delete tool while filter is active. | Tool becomes deselected. |
| 7 | Clear the search field. | All tools become visible again. |
| 8 | Verify all originally selected tools (that weren't manually changed) are still selected. | Original selections are **preserved**. |
| 9 | Verify the tool you selected during filter retains its new selected state. | Newly selected tool remains **selected**. |
| 10 | Verify the tool you deselected during filter retains its new deselected state. | Deselected tool remains **deselected**. |
| 11 | Verify total selected count is correct. | Count reflects actual selection state (original ± changes made during filter). |
| 12 | Save the toolkit and reopen it. | Toolkit saves and reopens successfully. |
| 13 | Verify selection persisted correctly after save. | All selection changes (including those made during filter) are **persisted**. |

## Expected Final State

All selection states (including changes made during search filter) are correctly saved and displayed.

## Pass/Fail Criteria

**Pass:**
- Search filtering is visual only — hidden tools retain their selection state
- Changes made to visible tools during filter are applied correctly
- Clearing search restores full view with correct selections
- Save persists all selection changes correctly

**Fail:**
- Search filtering modifies selection state of hidden tools
- Changes made during filter are lost when clearing search
- Selections are not preserved after save
