---
id: ELITEA-2649
title: "Default Modules Permissions and Access Control"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:settings, feat:modules, feat:permissions, eng:frontend, issue:6122, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6122]
---
# ELITEA-2649: Default Modules Permissions and Access Control

**Module:** Default Modules · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that Default Modules settings respect user permissions — users with appropriate roles can modify settings, while users without permissions have read-only access or no access to the settings.

**Coverage:**
- Project Admin/Editor can modify Default Modules settings 
- Users without edit permission (viewer) cannot modify Default Modules settings
- Permission checks are enforced on the backend

## Preconditions

- Logged into {{base_url}}
- Access to a Team project with multiple users having different roles
- Test accounts with different permission levels:
  - Project Admin account 
  - Project Editor account 
  - Project Viewer account
- Browser: Chrome/Firefox/Edge (latest)

## Test Data

Team project: Any Team project for testing
User roles:
- Editor/Admin: Settings edit permissions
- Viewer: Read-only or no settings access

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as Project Admin. | Successfully logged in. |
| 2 | Navigate to Team project → Settings → General → Default Modules. | Default Modules section is displayed. |
| 3 | Verify all toggles are interactive (can be clicked). | Admin can interact with all toggles. |
| 4 | Enable Image Creation for Chats. | Toggle switches to ON successfully. |
| 5 | Refresh the page and verify change persisted. | Change saved successfully. |
| 6 | Log out and log in as Project Editor/Admin (if role exists). | Successfully logged in. |
| 7 | Navigate to Team project → Settings → General → Default Modules. | Default Modules section is displayed. |
| 8 | Verify toggles are interactive for Editor/Admin. | Editor/Admin can interact with toggles (if permitted by role). |
| 9 | Attempt to change a toggle (e.g., enable Data Analysis). | Toggle changes successfully (or displays permission denied if role doesn't allow). |
| 10 | Log out and log in as Project Viewer (limited permissions). | Successfully logged in. |
| 11 | Navigate to Team project → Settings. | Settings page access behavior depends on permissions. |
| 12 | Attempt to access Default Modules section. | Either: (a) Section not visible, (b) Toggles are disabled/read-only, or (c) Settings page not accessible. |
| 13 | If toggles are visible but read-only, attempt to click a toggle. | Toggle does not change state. No error, but no action. |
| 14 | If Settings accessible, attempt to modify via browser DevTools (bypass UI). | Backend rejects the change with permission error (verify in Network tab). |

## Expected Final State

- Project Admin can fully modify Default Modules settings
- Users with edit permissions can modify settings (role-dependent)
- Users without edit permissions cannot modify settings
- Backend enforces permissions regardless of UI manipulation attempts

## Pass/Fail Criteria

**Pass:**
- Project Editor/Admin can modify all Default Modules settings
- Viewer/limited users cannot modify settings (UI prevents or backend rejects)
- Unauthorized changes are blocked at backend level

**Fail:**
- Admin cannot modify settings
- Users without permissions can modify settings
- Permission bypass possible through UI manipulation
- Backend does not enforce permission checks
