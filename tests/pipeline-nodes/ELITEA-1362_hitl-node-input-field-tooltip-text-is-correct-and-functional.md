---
id: ELITEA-1362
title: "HITL Node Input Field: Tooltip (ⓘ) Text Is Correct and Functional"
priority: medium
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1362: HITL Node Input Field: Tooltip (ⓘ) Text Is Correct and Functional

**Module:** Pipeline Nodes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the ⓘ info icon on the HITL node Input field shows an accurate, helpful tooltip with no placeholder or incorrect text.

**Coverage:**
- Tooltip appears on hover
- Text is accurate and explains the Input field purpose
- Tooltip disappears on mouse-out

## Preconditions

- Pipeline editor open; HITL node configuration panel open; Input field visible with ⓘ icon

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Locate the ⓘ icon next to the Input field label | ⓘ icon is visible |
| 2 | Hover the mouse over the ⓘ icon | A tooltip appears |
| 3 | Read the tooltip text | Tooltip text is accurate and explains the Input field; no 'TODO' or placeholder text |
| 4 | Move the mouse away from the icon | Tooltip disappears cleanly; no flicker or persistent tooltip |

## Expected Final State

Tooltip disappears cleanly; no flicker or persistent tooltip

## Pass/Fail Criteria

**Pass:**
- Tooltip present; text is accurate and helpful; disappears correctly

**Fail:**
- No tooltip on hover
- Empty or placeholder text
- Tooltip does not disappear
