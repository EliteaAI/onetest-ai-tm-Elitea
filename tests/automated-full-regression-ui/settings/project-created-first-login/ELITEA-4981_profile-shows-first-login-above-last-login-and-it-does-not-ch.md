---
id: ELITEA-4981
title: "Profile shows First login above Last login and it does not change when switching projects"
priority: critical
type: functional
module: settings
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

# ELITEA-4981: Profile shows First login above Last login and it does not change when switching projects

**Objective:** Settings → Profile shows the persisted **First login** directly above **Last login**, unaffected by the selected project.

## Preconditions

- User is logged in to `{{base_url}}` and has logged in more than once
- The user is a member of two team projects, **Team A** and **Team B**

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{project_id}/settings/profile` |
| Oracle | `GET {{base_url}}/api/v2/auth/user/default` → `id`, `name`, `email`, `first_login`, `last_login` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings → **Profile** | Fields in order: Full name, Email, User ID, **First login**, Last login |
| 2 | Call `auth/user/default` and compare it with the First login and Last login values | `first_login` (RFC 1123 GMT) is earlier than `last_login`; the UI First login equals `first_login` in local time, in the same format as Last login (en-US e.g. `5/18/2026, 12:51:50 PM`); First login differs from Last login |
| 3 | Compare Full name, Email, User ID and Last login with the API | All unchanged and equal to the API values |
| 4 | Switch the project in the sidebar to **Team A** | First login and Last login stay exactly the same in the UI and in the API |
| 5 | Switch to **Team B** | First login and Last login still stay exactly the same in the UI and in the API |

## Expected Final State

First login is shown per user, above Last login, and does not depend on the selected project.

## Pass/Fail Criteria

**Pass:**
- The field order is correct
- First login equals the API value and never changes on a project switch
- The existing Profile fields are unchanged

**Fail:**
- First login is missing, equals Last login, is placed elsewhere, or changes on a project switch
- Any existing Profile field changed

## Notes

- **Source functional tests:** ELITEA-4969 (`tests/elitea-platform/settings/project-created-first-login/`)
- **Regression rationale:** The core #7490 Profile behaviour: the new field, its position and its independence from the project. 1:1 with the source case.
- **Selected checkpoints:** field order; First login = API `first_login` in local time; First login ≠ Last login; existing fields unchanged; stable across two switches.
- **Selectors (`data-testid`):** `project-selector-trigger-combobox` (sidebar project switcher). The values sit next to the labels `First login:` / `Last login:` (the value is the label's next sibling).
- The Profile values are filled from `GET {{base_url}}/api/v2/social/author/`, which returns the same `first_login` as `auth/user/default`; either can be the oracle.
- Compute the expected value with `new Date(first_login).toLocaleString()` in the browser, not with a hard-coded string.
- For a user who existed before #7490, First login was backfilled from the Private project's creation time, so it equals Project created on the Private project. That is expected.
