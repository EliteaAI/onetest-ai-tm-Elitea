---
id: ELITEA-1331
title: "F-String Dropdown Not Triggered in State Modifier and Router Node Fields"
priority: medium
type: functional
module: pipeline-nodes
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2626]
---
# ELITEA-1331: F-String Dropdown Not Triggered in State Modifier and Router Node Fields

**Module:** Pipeline Nodes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the `{` keystroke does NOT trigger the F-String state variable dropdown in State Modifier (Jinja2 template) or Router (condition) node fields, since these use different templating syntax.

**Coverage:**
- `{` in State Modifier Template field does not trigger dropdown (Jinja2 uses `{{ }}`)
- `{` in Router condition field does not trigger dropdown
- Normal templating syntax in both nodes works without interference

## Preconditions

- Logged into {{base_url}}
- Pipeline with a State Modifier node and a Router node added to canvas

## Test Data

Typed input: `{` (single open brace)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the State Modifier node. Click inside the **Template** field. Type `{`. | No F-String state variable dropdown appears. The `{` character is accepted literally. |
| 2 | Type another `{` making `{{`. Continue typing a variable reference in Jinja2 style: `{{ project_id }}`. | Jinja2 template syntax is entered normally without any dropdown interference. |
| 3 | Click the Router node. Click inside the **condition** field. Type `{`. | No F-String state variable dropdown appears. Character is accepted literally. |

## Expected Final State

No F-String state variable dropdown appears. Character is accepted literally.

## Pass/Fail Criteria

**Pass:**
- No F-String dropdown appears in State Modifier Template or Router condition fields
- Normal Jinja2 and condition syntax works without disruption

**Fail:**
- F-String dropdown incorrectly appears in State Modifier or Router fields
