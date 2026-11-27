---
id: ELITEA-4981
title: "Team project Admin keeps access to Delete Project Data"
priority: critical
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

**Objective:** The private-owner change doesn't affect team projects: a team Admin still has Delete Project Data.

## Preconditions

- User A is logged in to `{{base_url}}` and is Admin of team project T. Accounts and API calls: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)

## Test Data

| Field | Value |
|-------|-------|
| Page | `{{base_url}}/app/{T id}/settings/project-general` |
| Users page | `{{base_url}}/app/{T id}/settings/users` |
| Delete probe | `GET` and `POST {"types": []}` on `{{base_url}}/api/v2/admin/project_data_delete/prompt_lib/{T id}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings → Users of T | User A's row shows the Admin role; `GET admin/users/default/{T id}` lists `admin` for User A |
| 2 | Open Settings → General of T | The **Delete Project Data** section is shown |
| 3 | Run the delete probe (GET, then POST with `{"types": []}`) | GET 200; POST 400 (authorized, nothing deleted) |

## Expected Final State

The team Admin's access is unchanged; nothing was deleted.

## Pass/Fail Criteria

**Pass:**
- User A is Admin of T, the section is shown, probe GET 200 / POST 400

**Fail:**
- The section is hidden for the team Admin, or the probe returns 403
