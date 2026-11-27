---
id: ELITEA-4964
title: "A viewer of a team project sees Project created as read-only"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

**Objective:** Project created is visible to project viewers and has no edit controls; existing permissions are unchanged.

## Preconditions

- **User B** has the **Viewer** role in team project **Team A**
- As a positive control, the Team A owner/admin sees an edit (pencil) icon in the General project header

## Test Data

| Field | Value |
|-------|-------|
| Role | Viewer |
| Oracle | `GET {{base_url}}/api/v2/elitea_core/project_info/prompt_lib/{project_id}/project-info` for Team A (called as User B) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User B, call `GET {{base_url}}/api/v2/elitea_core/project_info/prompt_lib/{project_id}/project-info` for Team A | HTTP 200 with `created_at` |
| 2 | As User B, select Team A and open Settings → **General** | Project created equals Team A's `created_at` in local time |
| 3 | Look for controls in the project header | No edit icon or button in the header; the Project created item has no input or button |

## Expected Final State

The viewer can read the creation date but cannot change anything.

## Pass/Fail Criteria

**Pass:**
- Project created shown and correct for the viewer
- No edit controls for the viewer

**Fail:**
- Project created hidden or wrong for the viewer, or an edit control appears
