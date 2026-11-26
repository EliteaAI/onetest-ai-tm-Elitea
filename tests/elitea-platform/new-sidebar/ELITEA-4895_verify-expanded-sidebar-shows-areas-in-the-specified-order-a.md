---
id: ELITEA-4895
title: "Verify expanded sidebar shows areas in the specified order and no standalone entity items"
priority: critical
type: functional
module: new-sidebar
status: ready
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4895: Verify expanded sidebar shows areas in the specified order and no standalone entity items


## Preconditions

- User is logged in to `{{base_url}}`
- User has a personal project with at least one chat
- Sidebar is expanded

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Viewport | 1366 × 768 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `{{base_url}}/app/` | The chat page opens with the sidebar expanded |
| 2 | Check the sidebar from top to bottom | The order is: Elitea logo and notification bell, project selector, **+ New chat**, **Artifacts**, **Explore**, **Chats** history area, bottom row |
| 3 | Look for standalone **Chats**, **Catalog**, **Agents**, **Pipelines**, **Skills**, **Toolkits**, **MCPs**, **Applications**, **Credentials** menu items | None of them appear as separate sidebar items |
| 4 | Check the bottom row | The bottom row contains **Settings**, **Help (?)** and **Support Assistant**, from left to right |

## Expected Final State

The expanded sidebar has the new structure, and the old entity navigation items are gone.

## Pass/Fail Criteria

**Pass:**
- All areas appear in the specified order
- No standalone entity or Catalog items are present

**Fail:**
- Any area is missing or out of order
- Any removed item is still shown in the sidebar
