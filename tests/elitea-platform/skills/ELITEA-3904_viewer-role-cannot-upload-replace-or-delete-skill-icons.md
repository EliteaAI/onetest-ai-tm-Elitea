---
id: ELITEA-3904
title: "Viewer role cannot upload replace or delete skill icons"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5699]
---

## Preconditions

- User is logged in to `{{base_url}}` as Viewer role in a team project
- At least one Skill exists in the project

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| User Role | Viewer |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as a Viewer user in a team project | Login successful |
| 2 | Navigate to the Skills page | Skills page loads |
| 3 | Open an existing Skill for viewing | Skill detail/view page opens |
| 4 | Locate the icon area in the form | Icon is displayed |
| 5 | Verify the icon picker is either not displayed or displayed with `editable={false}` | No edit capability visible |
| 6 | Attempt to click on the icon area | No SelectIconDialog opens |
| 7 | Verify there is no upload, replace, or delete icon option visible | No icon modification options present |

## Expected Final State

Viewer users cannot access icon upload functionality — no upload button is shown and no icon modification actions are available.

## Pass/Fail Criteria

**Pass:**
- Icon picker not clickable/editable for Viewer
- No upload button visible
- No SelectIconDialog opens on click

**Fail:**
- Viewer can open SelectIconDialog
- Upload button is visible to Viewer
- Viewer can modify icon
