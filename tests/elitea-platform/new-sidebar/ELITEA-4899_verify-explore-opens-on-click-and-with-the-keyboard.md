---
id: ELITEA-4899
title: "Verify Explore opens on click and with the keyboard"
priority: critical
type: functional
module: new-sidebar
status: ready
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4899: Verify Explore opens on click and with the keyboard


## Preconditions

- User is logged in to `{{base_url}}`
- Sidebar is expanded

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Input method | Mouse click; Keyboard (Tab + Enter/Space) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click **Explore** without hovering first (pointer enters and clicks immediately) | The section list opens |
| 2 | Click outside the list | The list closes |
| 3 | Move focus to **Explore** with Tab and press Enter (then Space) | The section list opens each time |
| 4 | Move through the list items with the keyboard and press Enter on **Agents** | The Agents page opens and the list closes |

## Expected Final State

The Agents section page is open.

## Pass/Fail Criteria

**Pass:**
- Explore opens by click and by keyboard, and a section can be opened from the keyboard

**Fail:**
- Explore only works on hover
- Keyboard focus can't reach Explore or its items
