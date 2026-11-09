---
id: ELITEA-4492
title: "Schedules — Admin Sees All, Editor Sees Own; Admin-Only Routes (API)"
priority: critical
type: regression
module: schedules
status: draft
execution_type: manual
tags: [automated:API:regression, feat:schedules, nfr:security, issue:7011, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7011"]
---

# ELITEA-4492: Schedules — Admin Sees All, Editor Sees Own; Admin-Only Routes (API)

**Module:** schedules · **Priority:** critical · **Type:** regression

**Objective:** Regression of role visibility and the admin-only routes, verified on stage2 on 2026-11-09 with an admin and an editor token. Complements elitea-api-testing `test_7011_schedule_access` (user2 vs user1). Manual source: ELITEA-4479, ELITEA-4486.

---

## Preconditions

- JWTs of a project **admin** and an **editor** of the same team project.
- Schedule **SA** owned by the admin, schedule **SE** owned by the editor.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Admin `GET …/schedules/prompt_lib/{project}`. | Both SA and SE; `run` in `allowed_actions` only for SA; `change_owner` on both. |
| 2 | Editor, same call. | Only SE; actions run, edit, pause, delete; no `change_owner`. |
| 3 | Editor `GET` / `PUT` / `pause` / `run` / `runs` / `DELETE` on SA. | 404 "Schedule not found" each; SA unchanged. |
| 4 | Editor `POST …/SA/owner` and `POST …/SE/owner`. | 403 `access_denied`, required `models.applications.schedules.admin`. |
| 5 | Editor `GET …/export?ids=SE`. | 403, required `models.applications.schedules.export`. |
| 6 | Editor `PUT …/settings`. | 403; `GET …/settings` → 200. |
| 7 | Admin `POST …/SE/run` `{"trigger":"manual"}`. | 403 `not_owner`. |
| 8 | Admin `POST …/SE/owner` `{"owner_id": 999999}`. | 400 "the new owner is not an active project member". |
| 9 | Check the 403 bodies of steps 4–6. | **Record**: they list the caller's full `current_permissions` (192 on stage2). |

---

## Expected Final State

No schedule changed.

## Teardown

None (read and refused calls only).
