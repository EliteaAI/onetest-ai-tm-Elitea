---
id: ELITEA-4959
title: "Switching projects updates Project created in Settings → General"
priority: critical
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

**Objective:** Project created follows the project selected in the sidebar without a page reload.

## Preconditions

- User is logged in to `{{base_url}}`
- The user is a member of at least two team projects (**Team A**, **Team B**) besides the Private project
- Settings → General is open on the Private project

## Test Data

| Field | Value |
|-------|-------|
| Projects | Private, Team A, Team B |
| Oracle | `GET {{base_url}}/api/v2/elitea_core/project_info/prompt_lib/{project_id}/project-info` for each project |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In the sidebar project switcher, select **Team A** | General reloads for Team A; Project created equals Team A's `created_at` in local time; Teammates equals Team A's `teammates_count` |
| 2 | Select **Team B** | Project created and Teammates change to Team B's values |
| 3 | Select **Private** again | Project created shows the Private project's value again |
| 4 | Check DevTools → Network | A `project-info` request was sent for each newly selected project |

## Expected Final State

Each project shows its own creation date; nothing stale from the previous project remains.

## Pass/Fail Criteria

**Pass:**
- The three projects show three different values, each equal to its API `created_at`

**Fail:**
- A previous project's value stays after switching, or the value does not match the API
