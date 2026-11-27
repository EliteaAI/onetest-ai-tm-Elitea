---
id: ELITEA-4980
title: "Project created shows for the Private project and follows project switching"
priority: critical
type: functional
module: settings
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

# ELITEA-4980: Project created shows for the Private project and follows project switching

**Objective:** Settings → General shows a read-only **Project created** date from the persisted creation time, and it follows the project selected in the sidebar.

## Preconditions

- User is logged in to `{{base_url}}`
- The user is a member of two team projects, **Team A** and **Team B**, besides their **Private** project
- The **Private** project is selected in the sidebar project switcher

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{project_id}/settings/project-general` |
| Projects | Private, Team A, Team B |
| Oracle | `GET {{base_url}}/api/v2/elitea_core/project_info/prompt_lib/{project_id}/project-info` → `created_at`, `teammates_count` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings → **General** for the Private project | The project header shows the project name, **Teammates:** and, after them, **Project created:** with a calendar icon |
| 2 | Call project-info for the Private project and compare `created_at` with the UI value | `created_at` is ISO 8601 with UTC offset and in the past; the UI value equals it in the browser's local time, formatted like Last login (en-US e.g. `5/18/2026, 12:51:50 PM`); it is not today and not the Last login date |
| 3 | Try to click or edit the Project created value | It is plain text: no input, no button, no edit affordance |
| 4 | In the sidebar project switcher, select **Team A** | Project created equals Team A's `created_at` in local time; Teammates equals Team A's `teammates_count` |
| 5 | Select **Team B** | Project created and Teammates change to Team B's values |
| 6 | Select **Private** again | Project created shows the Private project's value from step 2 again |

## Expected Final State

Each project shows its own creation date in the General header, read-only; nothing stale from the previous project remains.

## Pass/Fail Criteria

**Pass:**
- Project created is shown after Teammates and equals the API `created_at` in local time for each of the three projects
- The three values are different and the item is read-only

**Fail:**
- The item is missing, shows today/now or the Last login date, or is editable
- A previous project's value stays after switching, or a value does not match the API

## Notes

- **Source functional tests:** ELITEA-4967, ELITEA-4968 (`tests/elitea-platform/settings/project-created-first-login/`)
- **Regression rationale:** One journey covers the main #7490 General behaviour: the Private project's value and correct values after switching projects. All checkpoints of both source cases are kept.
- **Selected checkpoints:** placement after Teammates; value = API `created_at` in local time; read-only; one value per project; Teammates follows the project.
- **Selectors (`data-testid`):** `project-general-section` (General header), `project-selector-trigger-combobox` (sidebar project switcher; options are `role=option` with `data-value=<project_id>`).
- Compute the expected value in the browser with `new Date(created_at).toLocaleString()` — the same formatter as Last login — not with a hard-coded string.
- Switch projects with real clicks in the switcher, not a URL change. Expect one `project-info` GET per newly selected project.
- The Public project never shows Project created (by design in EliteaUI#1548), so do not use it as Team A or Team B.
