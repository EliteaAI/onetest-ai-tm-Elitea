---
id: ELITEA-3999
title: "Regression - Toolkit Sections Default States and Layout"
priority: critical
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, smoke, toolkit-sections-redesign, layout, feat:toolkits, r-2.0.8]
requirements: [EL-6252, EliteaAI/elitea_issues#7045]
---
# ELITEA-3999: Regression - Toolkit Sections Default States and Layout

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Regression / Smoke

**Objective:** Verify toolkit sections display with correct default states: Configuration expanded with all fields ("Show more" content already shown), Tools expanded with count, and icon-based view controls.

**Coverage:**
- Configuration section expanded by default
- Primary fields visible (Name, Description, Credentials dropdown)
- Additional ("Show more") fields visible by default; "Show less" link available (changed by EliteaAI/elitea_issues#7045)
- Tools section expanded with enabled/total count (changed by EliteaAI/elitea_issues#7045)
- Icon-based Form/Raw JSON view controls with tooltips

## Preconditions

- Logged in to {{base_url}}
- A toolkit with multiple tools exists
- Test is run in a fresh incognito window (no earlier collapse of the sections in this browser)

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
| 4 | Verify additional config fields and the "Show less" link are visible without clicking. | Additional config fields shown by default; "Show less" link present; no "Show more" link. |
| 5 | Click "Show less" → verify fields collapse. | Additional fields hidden; link changes to "Show more". |
| 6 | Click "Show more" → verify additional fields appear. | Additional config fields revealed with values unchanged. |
| 7 | Verify Tools section is expanded. | Tools section expanded by default with tool cards visible. |
| 8 | Verify Tools header shows count (e.g., "16 / 33"). | Enabled/total count displayed. |
| 9 | Verify view mode controls are icons, not text. | Icons for Form/Raw JSON views. |
| 10 | Hover over icons → verify tooltips appear. | "Form view" and "Raw JSON view" tooltips. |

## Expected Final State

Toolkit page displays correct default states for all sections with proper visual controls.

## Pass/Fail Criteria

**Pass:**
- Configuration expanded with primary and additional fields
- "Show less/more" works correctly
- Tools expanded with accurate count
- View mode icons with tooltips

**Fail:**
- Wrong default states (additional fields hidden or Tools collapsed on load)
- Missing fields or controls
- Incorrect counts
- Text labels instead of icons
