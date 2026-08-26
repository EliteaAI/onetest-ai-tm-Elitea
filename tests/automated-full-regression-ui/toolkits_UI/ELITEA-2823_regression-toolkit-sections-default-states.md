---
id: ELITEA-2823
title: "Regression - Toolkit Sections Default States and Layout"
priority: critical
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, smoke, toolkit-sections-redesign, layout]
requirements: [EL-6252]
---
# ELITEA-2823: Regression - Toolkit Sections Default States and Layout

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Regression / Smoke

**Objective:** Verify toolkit sections display with correct default states: Configuration expanded with primary fields, Tools collapsed with count, and icon-based view controls.

**Coverage:**
- Configuration section expanded by default
- Primary fields visible (Name, Description, Credentials dropdown)
- "Show more" link available
- Tools section collapsed with enabled/total count
- Icon-based Form/Raw JSON view controls with tooltips

## Preconditions

- Logged in to {{base_url}}
- A toolkit with multiple tools exists

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with tools (e.g., GitHub, ADO) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → open any toolkit. | Toolkit details page opens. |
| 2 | Verify Configuration section is expanded. | Configuration section expanded by default. |
| 3 | Verify primary fields visible: Name, Description, Credentials. | All 3 primary fields displayed; Credentials as dropdown. |
| 4 | Verify "Show more" link is visible. | Link present for additional fields. |
| 5 | Click "Show more" → verify additional fields appear. | Additional config fields revealed. |
| 6 | Click "Show less" → verify fields collapse. | Additional fields hidden. |
| 7 | Verify Tools section is collapsed. | Tools section collapsed by default. |
| 8 | Verify Tools header shows count (e.g., "16 / 33"). | Enabled/total count displayed. |
| 9 | Verify view mode controls are icons, not text. | Icons for Form/Raw JSON views. |
| 10 | Hover over icons → verify tooltips appear. | "Form view" and "Raw JSON view" tooltips. |

## Expected Final State

Toolkit page displays correct default states for all sections with proper visual controls.

## Pass/Fail Criteria

**Pass:**
- Configuration expanded with primary fields
- "Show more/less" works correctly
- Tools collapsed with accurate count
- View mode icons with tooltips

**Fail:**
- Wrong default states
- Missing fields or controls
- Incorrect counts
- Text labels instead of icons
