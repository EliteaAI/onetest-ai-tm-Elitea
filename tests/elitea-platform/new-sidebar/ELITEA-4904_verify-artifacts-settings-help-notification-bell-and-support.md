---
id: ELITEA-4904
title: "Verify Artifacts, Settings, Help, notification bell and Support Assistant work as before"
priority: high
type: regression
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4904: Verify Artifacts, Settings, Help, notification bell and Support Assistant work as before


## Preconditions

- User is logged in to `{{base_url}}`
- User has at least one unread notification

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Sidebar state | Expanded; Collapsed |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Check the notification bell | The unread indicator is shown |
| 2 | Click the bell | The notifications panel opens as on dev |
| 3 | Click **Artifacts** | The Artifacts page opens |
| 4 | Click **Settings** | The Settings page opens |
| 5 | Click **Help (?)** | The Help Center opens as on dev |
| 6 | Click **Support Assistant** | The Support Assistant opens and accepts a message |
| 7 | Collapse the sidebar and repeat steps 2–6 from the rail | Every control works the same way |

## Expected Final State

All preserved controls behave as on dev in both sidebar states.

## Pass/Fail Criteria

**Pass:**
- Each control opens its target in both states

**Fail:**
- Any control is missing, does nothing, or opens the wrong target
