---
id: ELITEA-3440
title: "Activity Tab Role Filter Excludes Super Admin and System Roles"
priority: medium
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [feat:monitoring, feat:roles-permissions, story:5110, regression]
requirements: [EliteaAI/elitea_issues#6794]
---
# ELITEA-3440: Activity Tab Role Filter Excludes Super Admin and System Roles

**Module:** Settings → Analytics · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm the role list/filter on the Team Analytics → Activity tab shows only project-scoped roles (Admin, Editor, Viewer, etc.) and excludes Super Admin and other system/tenant-level roles — regression check for #6794.

**Coverage:** Regression — [EliteaAI/elitea_issues#6794](https://github.com/EliteaAI/elitea_issues/issues/6794).

## Preconditions

- A project with at least one Super Admin (or other system-level role holder) and at least one project-scoped role (Admin/Editor/Viewer) with recorded activity

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the project's Team Analytics → Activity tab. | Page loads with the role list/filter (dropdown or column filter) visible. |
| 2 | Open the role list/filter and inspect every entry. | Only project-related roles are listed (e.g. Admin, Editor, Viewer). |
| 3 | Confirm Super Admin does not appear in the list, even though a Super Admin has activity recorded on the project. | Super Admin is absent from the role list. |
| 4 | Confirm no other system/tenant-level role (if any exist in this environment) appears in the list. | No system/tenant-level role appears. |

## Expected Final State

The Activity tab's role list contains only project-scoped roles; system-level roles are never shown, regardless of whether the role holder has activity on the project.

## Pass/Fail Criteria

**Pass:**
- Step 2's list contains only project-scoped roles
- Steps 3–4 confirm no system-level role is present

**Fail:**
- Super Admin or any other system/tenant-level role appears in the role list/filter
