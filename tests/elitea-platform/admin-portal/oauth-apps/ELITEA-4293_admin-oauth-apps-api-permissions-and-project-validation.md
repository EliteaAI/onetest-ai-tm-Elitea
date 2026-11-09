---
id: ELITEA-4293
title: "Admin OAuth apps API: permissions, project validation and hidden from generic configuration APIs"
priority: critical
type: security
module: admin-portal/oauth-apps
status: ready
execution_type: manual
tags: [feat:admin-platform, nfr:security, int:oauth, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4293: Admin OAuth apps API: permissions, project validation and hidden from generic configuration APIs

**Module:** admin-portal/oauth-apps · **Priority:** Critical · **Type:** Security

**Objective:** Verify that only Administration admins can manage OAuth apps, that the server enforces the required Projects and other field rules, and that app records can't be reached through the generic configuration APIs.

---

## Preconditions

- JWTs for: **Admin** (Administration admin), **User** (project editor, no Administration role).
- App **PUB** (Public) exists; note its `id` (uuid) and the Public project id.
- A team project pr_A and a personal project of User.

---

## Test Data

| Item | Value |
|------|-------|
| Base | `/api/v2/admin/oauth_apps/administration` |
| Check | `/api/v2/admin/oauth_app_check/administration[/{app_id}]` |
| Valid body | name, client_id, client_secret, oauth_discovery_endpoint, allowed_project_ids: [pr_A] |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User, open Admin Portal → Configuration. | OAuth Apps section not shown (or Admin Portal not reachable). |
| 2 | As User: GET, POST, PUT, DELETE on the base API and POST check. | 403 for every call. Nothing is created or changed. |
| 3 | (If a view-only admin role exists) open the section. | List visible. New, Edit and Delete disabled with "No permission to edit" / "No permission to delete". |
| 4 | As Admin, POST with `allowed_project_ids: []`. | 400 "Select at least one project". |
| 5 | POST check with `allowed_project_ids: []`. | 400 "Select at least one project". |
| 6 | PUT on PUB with `allowed_project_ids: []`. | 400. PUB keeps its project. |
| 7 | POST with `allowed_project_ids: [999999]`. | 400 "Unknown project: 999999". |
| 8 | POST without `client_secret`. | 400 "Client secret is required". |
| 9 | POST with `client_id: "  "`. | 400 "Client ID is required". |
| 10 | POST with `allowed_project_ids: [<Public id>, pr_A]`. | **Record.** Spec A3: 400 "An app is either for all projects (Public) or for selected team projects, not both". Not built: may be accepted (checklist G2). |
| 11 | In the dialog, open the Projects picker. | **Record** whether personal projects are offered and whether Public has a "Public" label. Spec: personal projects hidden (checklist G3). |
| 12 | As Admin, GET `/api/v2/configurations/configurations/{public_id}` and filter by type. | No `oauth_app` records in the result. |
| 13 | GET `/api/v2/configurations/configuration/{public_id}/{app_config_id}` for PUB. | Refused (404/403). No secret. |
| 14 | PUT and DELETE on that generic path. | Refused. PUB unchanged in the admin list. |
| 15 | POST a generic configuration with `type: "oauth_app"`. | Refused. |

---

## Postconditions

- Delete any app created by a step that was accepted.
