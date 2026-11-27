---
id: ELITEA-4993
title: "Run without approval schedule setting is changeable by the owner and Admin only"
priority: medium
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

**Objective:** The schedule setting "Run without approval" (permission `schedules.admin`) can be changed by the owner of a private project and a team Admin, and not by a team Editor.

## Preconditions

- User A (owner of P-A, Admin of T) and User B are available. Accounts, API calls and probes: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)
- User B is not a member of T
- DevTools → Network is open to watch for `PUT .../schedules/prompt_lib/.../settings` requests

## Test Data

| Caller | Project | "Run without approval" checkbox | Settings probe `PUT elitea_core/schedules/prompt_lib/{id}/settings` `{"qa_probe": true}` |
|---|---|---|---|
| User A (owner) | P-A | Enabled | 400 `field: qa_probe` |
| User A (Admin) | T | Enabled | 400 `field: qa_probe` |
| User B (Editor) | T | Absent or disabled | 403 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, call `GET elitea_core/schedules/prompt_lib/{P-A id}/settings` and note the result | 200 with the current settings |
| 2 | Open P-A's Settings → General and look at the Schedules section | The "Run without approval" checkbox is enabled. Don't change it |
| 3 | Run the settings probe on P-A, then repeat the GET from step 1 | Probe 400 `field: qa_probe`; settings are unchanged |
| 4 | Repeat steps 1–3 for T | Same result |
| 5 | As User A, add User B to T as Editor. As User B, open T's General and run the probe | Checkbox absent or disabled; probe 403; `GET auth/permissions/prompt_lib/{T id}` has no `models.applications.schedules.admin` |
| 6 | As User A, remove User B from T | B is no longer a member |

## Expected Final State

Schedule settings are unchanged in P-A and T, and the UI sent no settings save.

## Pass/Fail Criteria

**Pass:**
- Every row of the Test Data table matches, and settings are unchanged

**Fail:**
- The owner or team Admin can't change the setting, or the Editor can
