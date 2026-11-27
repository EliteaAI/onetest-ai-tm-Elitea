---
id: ELITEA-4994
title: "can_manage_settings matches the Delete Project Data section for every role"
priority: medium
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

**Objective:** The `can_manage_settings` flag behind the Settings UI gating is true exactly where the user is the private owner or an Admin, and the Delete Project Data section follows it.

## Preconditions

- User A (owner of P-A, Admin of T) and User B (owner of P-B) are available. Accounts and API calls: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)
- User A adds User B to T as **Editor**. B is not a member of P-A

## Test Data

Flag API: `GET {{base_url}}/api/v2/elitea_core/project_info/prompt_lib/{project_id}/project-info`

| Caller | Project | `can_manage_settings` | Delete Project Data section |
|---|---|---|---|
| User A (owner) | P-A | `true` | Shown |
| User A (Admin) | T | `true` | Shown |
| User B (owner) | P-B | `true` | Shown |
| User B (Editor) | T | `false` | Hidden |
| User B (no access) | P-A | HTTP 403 | Hidden |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | For each row, as that caller, call the flag API for the project | The value in the table |
| 2 | For each row, as that caller, open the project's Settings → General | The section matches the table |
| 3 | As User A, remove User B from T | B is no longer a member |

## Expected Final State

The section is shown exactly where `can_manage_settings` is true.

## Pass/Fail Criteria

**Pass:**
- Every row of the Test Data table matches

**Fail:**
- The flag is wrong for any role, or the section is shown or hidden against the flag
