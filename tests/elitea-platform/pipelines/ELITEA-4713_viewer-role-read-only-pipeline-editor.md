---
id: ELITEA-4713
title: "Viewer Role — Pipeline Editor Is Read-only (Panel, Node YAML, Duplicate, Pickers)"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7157, EliteaAI/elitea_issues#7158, EliteaAI/elitea_issues#7159, EliteaAI/elitea_issues#7161, EliteaAI/elitea_issues#7407]
---
# ELITEA-4713: Viewer Role — Pipeline Editor Is Read-only (Panel, Node YAML, Duplicate, Pickers)

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that a user with the Viewer role cannot change a pipeline: page actions are hidden, node panel fields are disabled, the node YAML editor is read-only (Find/Copy allowed, Replace disabled), Duplicate is unavailable and nothing can be attached or detached.

**Coverage:**
- Save / Save As Version / Discard hidden
- Node panel fields and footer actions disabled/hidden
- Node YAML: read-only, Find + Copy work, Replace disabled
- Duplicate unavailable
- Pickers / X-clear can't attach or detach
- Regression for elitea_issues#7407 (fixed)
- See ELITEA-4721 for the main flow

## Preconditions

- Logged in to {{base_url}} as a **separate viewer-role account** in the same project as the pipeline
- A pipeline with Agent, Toolkit and MCP nodes owned by another user

## Test Data

- None

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline. | Save, Save As Version and Discard are not shown. |
| 2 | Click a node to open its panel; try to edit Name, a select and a text field. | All fields are disabled; footer actions Duplicate and Delete are hidden (not present); Make Entrypoint and Edit with AI are not available. |
| 3 | Switch the panel to **YAML**; try to type. | Typing is blocked. |
| 4 | Press Ctrl/Cmd+F and search. | Find works. |
| 5 | Click the Copy icon. | Node YAML is copied. |
| 6 | Press Ctrl/Cmd+H. | Replace is disabled. |
| 7 | Check the panel footer for Duplicate and Delete. | Duplicate and Delete icons are hidden — not present in the footer. |
| 8 | Try to open a node picker or click ✕ next to an attached toolkit. | Nothing can be attached or detached; TOOLS unchanged. |
| 9 | Try to drag a node or connect nodes on the canvas. | No change can be made/persisted. |

## Expected Final State

A Viewer can view the pipeline and read/copy YAML, but cannot edit, duplicate, attach/detach or save anything.

## Pass/Fail Criteria

**Pass:**
- Page actions hidden; all panel fields read-only
- Node YAML read-only with Find/Copy working and Replace disabled
- Duplicate and attach/detach unavailable

**Fail:**
- Any field or the node YAML is editable for a viewer
- Replace, Duplicate or attach/detach is possible
- Save / Discard visible to a viewer
