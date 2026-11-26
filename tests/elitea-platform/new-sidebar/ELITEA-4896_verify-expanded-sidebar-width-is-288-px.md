---
id: ELITEA-4896
title: "Verify expanded sidebar width is 288 px"
priority: critical
type: functional
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4896: Verify expanded sidebar width is 288 px


## Preconditions

- User is logged in to `{{base_url}}`
- Sidebar is expanded

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Viewport | 1366 × 768 and 1920 × 1080 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `{{base_url}}/app/` | The page opens with the sidebar expanded |
| 2 | Open DevTools and inspect the sidebar container | The sidebar container is selected |
| 3 | Read the computed width of the sidebar | The width is **288 px** (not 216 px) |
| 4 | Repeat steps 1–3 at the second viewport | The width stays **288 px** |

## Expected Final State

The expanded sidebar is 288 px wide at the supported viewports.

## Pass/Fail Criteria

**Pass:**
- Computed width is 288 px at every listed viewport

**Fail:**
- Width is 216 px or any other value
