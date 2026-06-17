---
id: ELITEA-1024
title: "Outlined Icons Applied Correctly to All Four Fixed Menu Items [Parametrized]"
priority: high
type: functional
module: sidebar-menu
status: ready
execution_type: manual
tags: [nfr:usability, r-2.0.1, 3846]
requirements: [ProjectAlita/projectalita.github.io#3846]
---
# ELITEA-1024: Outlined Icons Applied Correctly to All Four Fixed Menu Items [Parametrized]

**Module:** Sidebar Menu · **Priority:** High · **Type:** Functional

**Objective:** Verify that Applications, Personalization, Analytics, and Environment menu items all display the new outlined-style icon consistent with the rest of the sidebar design.

**Coverage:**
- Applications icon uses outlined style
- Personalization icon uses outlined style
- Analytics icon uses outlined style
- Environment icon uses outlined style (Public project)
- All icons are visually consistent (no mixture of filled and outlined styles)

## Preconditions

- User is logged in to ELITEA
- Access to a Private/Team project (for Applications, Personalization, Analytics)
- Access to a Public project (for Environment)

## Test Data

| # | Menu Item | Project Type |
|---|---|---|
| 1 | Applications | Private/Team |
| 2 | Personalization | Private/Team |
| 3 | Analytics | Private/Team |
| 4 | Environment | Public |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to a Private/Team project in ELITEA. | Project loads. |
| 2 | Expand the sidebar and locate the Applications icon. | Icon is visible. |
| 3 | Visually inspect the Applications icon: it must use an outlined (line-art, not filled/solid) icon style — comparable to the outlined style of Chat, Agents, Pipelines icons. | Applications icon displays the outlined icon as specified in issue EliteaAI/elitea_issues#3846 (not the old filled icon). |
| 4 | Repeat steps 2–3 for Personalization icon. | Personalization icon displays the correct outlined icon. |
| 5 | Repeat steps 2–3 for Analytics icon. | Analytics icon displays the correct outlined icon. |
| 6 | Switch to a Public project. Locate the Environment icon. | Environment icon is visible. |
| 7 | Visually inspect the Environment icon for outlined style. | Environment icon displays the correct outlined icon. |
| 8 | Compare all four icons against the remaining sidebar icons (Chat, Agents, Pipelines, etc.) for visual consistency — all should share the same icon style family. | All sidebar icons appear visually consistent in style. |

## Expected Final State

All sidebar icons appear visually consistent in style.

## Pass/Fail Criteria

**Pass:**
- All four icons (Applications, Personalization, Analytics, Environment) use outlined style
- Icon style is consistent with the rest of the sidebar icons

**Fail:**
- Any of the four icons still shows the old filled/solid style
- Any icon appears pixelated, blurry, or misaligned
- Icon design is inconsistent with the other sidebar items
