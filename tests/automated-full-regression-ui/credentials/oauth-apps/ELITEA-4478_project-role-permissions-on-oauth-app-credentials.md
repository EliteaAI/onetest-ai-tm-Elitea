---
id: ELITEA-4478
title: "OAuth Apps — Project Role Permissions on Default App Credentials"
priority: critical
type: regression
module: toolkits-credentials/oauth-apps
status: draft
execution_type: manual
tags: [automated:API:regression, feat:credentials, nfr:security, int:outlook, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4478: OAuth Apps — Project Role Permissions on Default App Credentials

**Module:** toolkits-credentials/oauth-apps · **Priority:** critical · **Type:** regression

**Objective:** Regression of the viewer / editor / admin permissions on Default app credentials, without a Microsoft sign-in. Manual source: ELITEA-4475.

---

## Preconditions

- One enabled app on Project 1 marked **Default** (by admin API).
- JWTs of a **viewer**, an **editor** and a **project admin** of one team project.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As each role, `GET /api/v2/configurations/oauth_apps/{project}?type=outlook`. | 200 for all 3, `mode: "default"`, no `client_secret`. |
| 2 | As viewer, POST an Outlook credential `{oauth_app_id: <app>}`. | 403. |
| 3 | As editor, POST the same credential. | 201. Response/GET has `oauth_app_id`, no secret. |
| 4 | As viewer, GET the credential. | 200, no secret. |
| 5 | As viewer, PUT and DELETE it. | 403. |
| 6 | As editor, PUT with a new display name. | 200. |
| 7 | As editor, PUT with a `refresh_token` value. | 403 "Only project admins can log in or out on a team credential". |
| 8 | As admin, PUT with a `refresh_token` value, then without it. | 200 both times. |
| 9 | As editor, PUT with `shared: true`. | 400 "Outlook credentials cannot be shared". |
| 10 | As each role, GET `/api/v2/admin/oauth_apps/administration`. | 403 for all (not platform admins). |
| 11 | As admin, DELETE the credential. | 200. |

---

## Expected Final State

No test credential remains. Every role got only the access listed above.
