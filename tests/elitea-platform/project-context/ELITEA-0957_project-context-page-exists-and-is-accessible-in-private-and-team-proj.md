---
id: ELITEA-0957
title: "Project Context Page Exists and Is Accessible in Private and Team Projects"
priority: critical
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, private-project, feat:settings, team-project, permissions, story:3395, issue:3395, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0957: Project Context Page Exists and Is Accessible in Private and Team Projects

**Module:** Project Context · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Project Context page is present in Project Settings for both Private and Team projects and is accessible to all user roles.

**Coverage:**
- Project Context page visible in Private project Settings
- Project Context page visible in Team project Settings
- Page loads without errors for Admin, Editor, and Viewer users

## Preconditions

- Logged into {{base_url}}
- A Private project exists with Admin, Editor, and Viewer member roles
- A Team project exists with Admin, Editor, and Viewer member roles
- Feature flag for Project Context is enabled in the environment

## Test Data

- Private Project URL: {{base_url}}
- Team Project: any existing team project
- Roles: admin@test.com, editor@test.com, viewer@test.com

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as Admin. Navigate to a Private project. Open Settings from the sidebar. | Settings page opens successfully. |
| 2 | Look for 'Project Context' in the Settings sidebar navigation. | 'Project Context' menu item is visible in Project Settings navigation. |
| 3 | Click on 'Project Context'. | Project Context page loads without errors. Page shows editor area, enable toggle, and upload option. |
| 4 | Repeat steps 1-3 for a Team project (as Admin). | Project Context page is also present and loads correctly in Team project settings. |
| 5 | Log out and log in as Editor. Navigate to the Private project → Settings → Project Context. | Editor can access the page; content is shown in read-only mode. |
| 6 | Log out and log in as Viewer. Navigate to the Private project → Settings → Project Context. | Viewer can access the page; content is shown in read-only mode. |
| 7 | Log out and log in as a user who is NOT a member of the project. Attempt to navigate directly to the Project Context settings URL. | Page is inaccessible — user is redirected or shown a 403/unauthorized error. |

## Expected Final State

Page is inaccessible — user is redirected or shown a 403/unauthorized error.

## Pass/Fail Criteria

**Pass:**
- Project Context page exists under Settings for both project types
- All three roles can open the page without errors
- Non-members cannot access the page

**Fail:**
- Project Context page is missing from Settings
- Page shows an error for any valid role
- Non-member can access the page
