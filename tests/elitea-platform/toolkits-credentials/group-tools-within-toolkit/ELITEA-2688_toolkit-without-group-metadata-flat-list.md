---
id: ELITEA-2688
title: "Toolkit Without Group Metadata Renders Flat List (No Regression)"
priority: critical
type: functional
module: toolkits-credentials/group-tools-within-toolkit
status: ready
execution_type: manual
tags: [feat:toolkits, tools, mcp-toolkit, regression]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2688: Toolkit Without Group Metadata Renders Flat List (No Regression)

**Module:** Toolkits Credentials / Group Tools Within Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify toolkits whose tools carry no group metadata (e.g., MCP toolkits) fall back to the current flat list behavior without grouping UI.

**Coverage:**
- MCP toolkits display flat alphabetical tool list
- No grouping UI (headers, badges, counts) is shown
- Tool selection/deselection works as before
- Saving preserves tool selections correctly
- No regression in MCP toolkit behavior

## Preconditions

- Logged in to {{base_url}}
- User has access to ELITEA platform
- An MCP toolkit exists and is configured
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an MCP toolkit configuration. | Toolkit configuration page opens. |
| 2 | Navigate to Tools section. | Tools section displays. |
| 3 | Verify tools are displayed as a flat alphabetical list (no grouping). | Tools appear in a **flat alphabetical list** without group headers. |
| 4 | Verify NO group headers are shown (Read, Create & update, Delete, Execute). | Group headers are **absent**. |
| 5 | Verify NO group badges are shown. | No Read-only, Changes data, Destructive, or Unrestricted badges. |
| 6 | Select several tools by clicking their checkboxes. | Tools become selected, visual indicator updates. |
| 7 | Deselect several tools by clicking their checkboxes. | Tools become deselected, visual indicator updates. |
| 8 | Save the toolkit. | Toolkit saves successfully. |
| 9 | Reopen the toolkit and verify tool selections. | All selected tools are **preserved correctly**. Deselected tools remain deselected. |

## Expected Final State

MCP toolkit displays flat tool list and preserves all selections after save.

## Pass/Fail Criteria

**Pass:**
- MCP toolkits display flat alphabetical tool list
- No grouping UI (headers, badges, counts) is shown
- Tool selection/deselection works correctly
- Saving preserves tool selections
- No regression in MCP toolkit behavior

**Fail:**
- MCP toolkit displays grouping UI
- Group headers or badges appear on MCP toolkit
- Tool selection/deselection does not work
- Selections are not preserved after save
