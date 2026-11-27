---
id: ELITEA-4958
title: "Settings → General shows Project created for the Private project"
priority: critical
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

**Objective:** The Private project's header in Settings → General shows a read-only **Project created** date taken from the persisted creation time.

## Preconditions

- User is logged in to `{{base_url}}`
- The user's **Private** project is selected in the sidebar project switcher

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{project_id}/settings/project-general` |
| Oracle | `GET {{base_url}}/api/v2/elitea_core/project_info/prompt_lib/{project_id}/project-info` → `created_at` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings → **General** for the Private project | The project header shows the project name, **Teammates:** and, after them, **Project created:** with a calendar icon |
| 2 | Read the Project created value | A date and time formatted like **Last login** (browser locale and time zone, e.g. en-US `5/18/2026, 12:51:50 PM`) |
| 3 | Call `GET {{base_url}}/api/v2/elitea_core/project_info/prompt_lib/{project_id}/project-info` for the Private project | `created_at` is present, ISO 8601 with UTC offset, and in the past |
| 4 | Compare the UI value with `created_at` | The UI value equals `created_at` converted to the browser's local time; it is not today and not the Last login date |
| 5 | Try to click or edit the Project created value | It is plain text: no input, no button, no edit affordance |

## Expected Final State

The Private project's creation date is shown read-only in the General header.

## Pass/Fail Criteria

**Pass:**
- Project created is shown after Teammates and equals the API `created_at` in local time
- The value is read-only

**Fail:**
- The item is missing, shows today/now or the Last login date, or is editable
