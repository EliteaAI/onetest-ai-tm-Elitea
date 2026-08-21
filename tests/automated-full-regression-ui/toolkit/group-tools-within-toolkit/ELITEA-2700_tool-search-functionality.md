---
id: ELITEA-2700
title: "Tool Search Filters, Preserves Selection, and Shows Correct Counts"
priority: critical
type: functional
module: toolkit/group-tools-within-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, tools, search, filter, selection]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2700: Tool Search Filters, Preserves Selection, and Shows Correct Counts

**Module:** Toolkit / Group Tools Within Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify tool search filters correctly, preserves selections during filtering, maintains accurate counts, and persists changes after save.

**Coverage:**
- Search placeholder "Search tools"
- Case-insensitive search matching display name and raw tool name
- Groups hidden when no matching tools
- Empty state message for zero results
- Counts reflect total group (not filtered subset)
- Selections preserved during and after filtering
- Changes made during filter persist after save

## Preconditions

- Logged in to {{base_url}}
- SDK toolkit with 30+ tools exists (e.g., GitHub)
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a toolkit with 30+ tools. Locate search field at top of Tools section. | Search field visible, **empty** by default, placeholder **"Search tools"**. |
| 2 | Type **"read"** (lowercase) in search field. | Tools matching "read" are shown (display name or raw name). |
| 3 | Clear and type **"READ"** (uppercase). | **Same results** — search is **case-insensitive**. |
| 4 | Clear and type **"file"**. | Tools matching "file" shown across multiple groups. |
| 5 | Verify groups without matching tools are hidden. | Only groups with matches are visible. Empty groups **hidden**. |
| 6 | Note the count in a visible group header (e.g., Read shows "10 / 26"). | Count reflects **total group** composition, not filtered subset. |
| 7 | Clear and type **"xyzno123"**. | Message: **'No tools match "xyzno123"'**. No tools displayed. Inline styling. |
| 8 | Clear search field. Note some tools are selected (e.g., 8 total). | All tools reappear. **Original selections preserved**. |
| 9 | Type a filter term (e.g., **"delete"**). Select one additional tool while filtered. Deselect another. | Visible tools can be selected/deselected. |
| 10 | Clear search field. | Hidden tools still have **original selection state**. Changes made during filter **retained**. |
| 11 | Save the toolkit and reopen it. | All selections (including changes made during filter) are **persisted**. |

## Expected Final State

Search works correctly, selections preserved, counts accurate, changes persist.

## Pass/Fail Criteria

**Pass:**
- Placeholder "Search tools"
- Case-insensitive search
- Matches display name and raw tool name
- Empty groups hidden during search
- Empty state message shown for no matches
- Counts reflect total group (not filtered)
- Selections preserved during/after filtering
- Changes made during filter persist after save

**Fail:**
- Search case-sensitive
- Doesn't match raw tool names
- Empty groups remain visible
- Counts change to reflect filtered subset
- Selections lost during/after filtering
- Changes not persisted
