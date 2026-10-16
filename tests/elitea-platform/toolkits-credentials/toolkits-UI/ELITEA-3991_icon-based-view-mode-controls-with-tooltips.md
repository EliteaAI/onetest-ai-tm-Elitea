---
id: ELITEA-3991
title: "Icon-Based View Mode Controls with Tooltips"
priority: high
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-sections-redesign, configuration, view-controls, icons]
requirements: [EL-6252]
---
# ELITEA-3991: Icon-Based View Mode Controls with Tooltips

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify that Form/Raw JSON view controls use icons instead of text labels, with accessible tooltips and clear selection indication.

**Coverage:**
- View controls displayed as icons, not text labels
- Form view icon clearly identifiable
- Raw JSON/code icon clearly identifiable
- Tooltips display on hover
- Selected view state clearly indicated

## Preconditions

- Logged in to {{base_url}}
- A toolkit exists with configuration data

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any existing toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → open any toolkit. | Toolkit details page opens. |
| 2 | Locate the view mode controls near the Configuration section (breadcrumb area). | View mode controls visible. |
| 3 | Verify controls are displayed as icons, NOT text "Form \| Raw JSON". | Icons displayed instead of text labels. |
| 4 | Identify the Form view icon (form/list icon). | Form view icon is recognizable. |
| 5 | Identify the Raw JSON view icon (code/JSON icon). | JSON view icon is recognizable. |
| 6 | Hover over the Form view icon. | Tooltip displays "Form view". |
| 7 | Hover over the Raw JSON view icon. | Tooltip displays "Raw JSON view". |
| 8 | Verify the currently selected view is clearly indicated. | Selected icon has distinct styling (highlighted, bordered, or filled). |
| 9 | Click the Raw JSON icon. | View switches to Raw JSON editor. |
| 10 | Verify Raw JSON icon now shows as selected. | Raw JSON icon has selected state styling. |
| 11 | Click the Form icon. | View switches back to Form view. |
| 12 | Verify Form icon now shows as selected. | Form icon has selected state styling. |

## Expected Final State

View controls use icons with working tooltips, and the selected view is clearly indicated visually.

## Pass/Fail Criteria

**Pass:**
- Icons displayed instead of "Form | Raw JSON" text
- Tooltips show "Form view" and "Raw JSON view"
- Selected state clearly distinguishable
- Clicking icons switches views correctly

**Fail:**
- Text labels "Form | Raw JSON" still displayed
- No tooltips on hover
- Selected state not visible or unclear
- Icons don't switch views
