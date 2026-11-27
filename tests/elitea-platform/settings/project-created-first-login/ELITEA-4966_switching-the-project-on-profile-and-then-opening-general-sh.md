---
id: ELITEA-4966
title: "Switching the project on Profile and then opening General shows the new project's Project created"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

**Objective:** Navigating Profile ↔ General with a project switch in between never shows a stale Project created.

## Preconditions

- User is logged in to `{{base_url}}` and is a member of a team project **Team B**
- Settings → General is open on the Private project

## Test Data

| Field | Value |
|-------|-------|
| Oracle | `GET {{base_url}}/api/v2/elitea_core/project_info/prompt_lib/{project_id}/project-info` for Private and Team B; `GET {{base_url}}/api/v2/auth/user/default` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Note Project created on General (Private) | Equals the Private `created_at` |
| 2 | Open the **Profile** tab in the Settings drawer | First login equals the API `first_login` |
| 3 | While on Profile, switch the project to Team B in the sidebar | The page stays on Profile; First login is unchanged |
| 4 | Open the **General** tab | Project created shows Team B's `created_at`, not the Private value |
| 5 | Open **Profile** again | First login is still unchanged |

## Expected Final State

General always reflects the currently selected project; First login never changes.

## Pass/Fail Criteria

**Pass:**
- Team B's date is shown after the switch made on Profile
- First login constant throughout

**Fail:**
- General shows the Private project's stale date, or First login changes
