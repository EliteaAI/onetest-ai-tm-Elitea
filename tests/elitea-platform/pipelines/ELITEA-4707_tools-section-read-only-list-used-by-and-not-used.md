---
id: ELITEA-4707
title: "Left TOOLS Section — Read-only List, Used By, Not Used by Any Node, Log In"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7159]
---
# ELITEA-4707: Left TOOLS Section — Read-only List, Used By, Not Used by Any Node, Log In

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that the left TOOLS section is read-only (no add buttons), lists attached items with icon, name, version, status and Used by, lets the user jump to a using node, keeps orphaned attachments labelled "Not used by any node", and leaves Modules unchanged.

**Coverage:**
- No + Toolkit / + MCP / + Agent / + Pipeline buttons
- Empty state text
- Item: icon, name, version (agents/pipelines), health/auth status, Log in for MCP
- Used by: node names, click selects node and opens its panel
- Show tools (read-only)
- Orphaned attachment: "Not used by any node", stays attached
- Items are listed flat (grouping by type accepted as a future enhancement)
- Modules (Attachments) unchanged

## Preconditions

- Logged in to {{base_url}}
- A pipeline using a toolkit (2 nodes), an MCP needing login, an agent and a pipeline
- An older pipeline with an attachment no node uses

## Test Data

- None

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new pipeline; look at the TOOLS section in the left side panel. | *"Tools you select in nodes will appear here."*; no + Toolkit / + MCP / + Agent / + Pipeline buttons. |
| 2 | Open the pipeline with attached items; look at TOOLS. | Each item shows type icon and name; agents/pipelines also show their version (e.g. `base`). Items are listed flat (not grouped by type — accepted). |
| 3 | Observe the toolkit used by 2 nodes. | *"Used by: <node 1>, <node 2>"*. |
| 4 | Click a node name in Used by. | That node is selected on the canvas and its panel opens. |
| 5 | Observe the MCP needing login; click **Log in**. | Status/auth state shown with **Log in**; login completes successfully. |
| 6 | Click **Show tools** on an item. | Read-only list of the selected tools; no editing possible from here. |
| 7 | Open the older pipeline with an unused attachment. | That item shows a muted **"Not used by any node"** label and remains attached (not auto-removed). |
| 8 | Observe MODULES. | Attachments toggle unchanged. |

## Expected Final State

The TOOLS section is a read-only overview of attachments, populated only via nodes, showing usage and status, with orphaned attachments clearly labelled.

## Pass/Fail Criteria

**Pass:**
- No add buttons; correct empty state
- Item details, Used by and jump-to-node work
- Log in for MCP works; Show tools is read-only
- Orphaned attachment labelled and kept

**Fail:**
- Any add button present
- Used by missing/incorrect or not clickable
- Orphaned attachment removed automatically or not labelled
