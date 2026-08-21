---
id: ELITEA-2695
title: "Tool Search Filters Tools by Display Name and Raw Tool Name"
priority: critical
type: functional
module: toolkits-credentials/group-tools-within-toolkit
status: ready
execution_type: manual
tags: [feat:toolkits, tools, search, filter, empty-state]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2695: Tool Search Filters Tools by Display Name and Raw Tool Name

**Module:** Toolkits Credentials / Group Tools Within Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the search field performs case-insensitive substring matching against both the display label and the raw tool name, has correct placeholder, and shows appropriate empty state.

**Coverage:**
- Search field has correct placeholder text "Search tools"
- Search matches against both display name and raw tool name
- Search is case-insensitive
- Only matching tools are displayed during search
- Groups without matching tools are hidden
- Empty state message 'No tools match "[search term]"' shown for zero results (styled non-intrusively)
- Clearing search restores full tool list with preserved selections

## Preconditions

- Logged in to {{base_url}}
- User has access to ELITEA platform
- SDK toolkit with 30+ tools exists (e.g., GitHub)
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a toolkit with 30+ tools (e.g., GitHub) and locate the search field at the top of the Tools section. | Search field is visible above the tool groups. Field is **empty** by default. |
| 2 | Verify search field placeholder text. | Placeholder text is **"Search tools"**. |
| 3 | Type **"read"** (lowercase) in the search field. | Tools matching "read" are shown: Read file, Read multiple files, read_file, read_multiple_files, etc. |
| 4 | Clear and type **"READ"** (uppercase) in the search field. | **Same results** as "read" — search is **case-insensitive**. |
| 5 | Clear and type **"file"** in the search field. | Tools matching "file" are shown: Read file, Create file, Delete file, Update file, etc. |
| 6 | Clear and type **"read_f"** (partial raw name) in the search field. | Tools with raw name matching "read_f" are shown (e.g., read_file). |
| 7 | Clear and type **"ISSUe"** in the search field. | Tools matching "issue" are shown: Get issue, Create issue, Update issue, Search issues, etc. |
| 8 | Verify that group headers are hidden when all their tools are filtered out. | Only groups with matching tools are displayed. Empty groups are hidden. |
| 9 | Clear and type **"xyznonexistent123"** (no matches expected) in the search field. | Message displays: **'No tools match "xyznonexistent123"'**. No tools are displayed. All group headers are hidden. |
| 10 | Verify empty state message styling. | Message is styled **non-intrusively** as inline text (not a modal or alert). |
| 11 | Clear the search field completely. | **All tools reappear** with original selection state preserved. All groups are visible again. |

## Expected Final State

Search field is empty, all tools are visible, original selection state is preserved.

## Pass/Fail Criteria

**Pass:**
- Search field placeholder is "Search tools"
- Search matches against both display name and raw tool name
- Search is case-insensitive
- Only matching tools are displayed during search
- Groups without matching tools are hidden
- Empty state message format is 'No tools match "[search term]"' (styled non-intrusively)
- Clearing search restores full tool list with preserved selections

**Fail:**
- Search field has incorrect or no placeholder
- Search does not match raw tool names
- Search is case-sensitive
- Groups with no matching tools remain visible
- Empty state message is missing, incorrectly formatted, or styled as modal/alert
- Clearing search does not restore all tools or loses selections
