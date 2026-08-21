---
id: ELITEA-2703
title: "MCP Toolkit Displays Flat List Without Grouping"
priority: critical
type: functional
module: toolkit/group-tools-within-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, tools, mcp-toolkit, regression]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2703: MCP Toolkit Displays Flat List Without Grouping

**Module:** Toolkit / Group Tools Within Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify MCP toolkits (without group metadata) display tools as a flat alphabetical list without grouping UI.

**Coverage:**
- MCP toolkit shows flat tool list (no group headers)
- No badges (Read-only, Changes data, etc.)
- Tools in alphabetical order
- Selection works correctly
- Persistence works correctly

## Preconditions

- Logged in to {{base_url}}
- An MCP toolkit exists and is configured
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an MCP toolkit configuration. | Toolkit configuration opens. |
| 2 | Navigate to Tools section. | Tools section displays. |
| 3 | Verify tools are displayed as a flat list (no grouping). | Tools appear in **flat alphabetical list** without group headers. |
| 4 | Verify NO group headers shown (Read, Create & update, Delete, Execute). | Group headers are **absent**. |
| 5 | Verify NO group badges shown. | No Read-only, Changes data, Destructive, Unrestricted badges. |
| 6 | Verify tools are in alphabetical order. | Tools sorted **A-Z**. |
| 7 | Select several tools. | Tools become selected. |
| 8 | Deselect some tools. | Tools become deselected. |
| 9 | Save the toolkit. | Save completes successfully. |
| 10 | Reopen the toolkit. | Selections are **preserved correctly**. |

## Expected Final State

MCP toolkit displays flat tool list and preserves selections after save.

## Pass/Fail Criteria

**Pass:**
- Flat alphabetical tool list (no grouping)
- No group headers or badges
- Selection works
- Persistence works

**Fail:**
- Grouping UI appears on MCP toolkit
- Headers or badges displayed
- Selection doesn't work
- Selections not preserved
