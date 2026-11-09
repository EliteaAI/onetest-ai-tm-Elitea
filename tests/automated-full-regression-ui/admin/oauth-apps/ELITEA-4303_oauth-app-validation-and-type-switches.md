---
id: ELITEA-4303
title: "OAuth Apps — Server Validation and Credential Type Switches"
priority: high
type: regression
module: admin-portal/oauth-apps
status: draft
execution_type: manual
tags: [automated:API:regression, feat:admin-platform, nfr:security, int:oauth, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4303: OAuth Apps — Server Validation and Credential Type Switches

**Module:** admin-portal/oauth-apps · **Priority:** high · **Type:** regression

**Objective:** Regression of the server-side checks on the admin OAuth apps API and of the per-type switches. Manual source: ELITEA-4291, ELITEA-4293.

---

## Preconditions

- JWT of an Administration admin and of a project user with no Administration role.
- A valid app body: name, client_id, client_secret, `allowed_project_ids: [<team project>]`.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As the project user, GET and POST `/api/v2/admin/oauth_apps/administration`. | 403 for both. |
| 2 | As admin, POST with `allowed_project_ids: []`. | 400 "Select at least one project". |
| 3 | POST with an unknown project id. | 400 "Unknown project: <id>". |
| 4 | POST without `client_secret`. | 400 "Client secret is required". |
| 5 | POST with endpoint `https://example.com/tenant`. | 400: the endpoint must be on `login.microsoftonline.com`. |
| 6 | POST with `credential_types: []`. | 400 "Enable at least one credential type for this app". |
| 7 | POST with `scopes: {"jira": ["read"]}`. | 400 "Microsoft Entra ID apps have no scopes for: jira". |
| 8 | POST the valid body with `credential_types: ["sharepoint"]`. | 201. Response has `credential_types: ["sharepoint"]`, `client_secret_set: true`, no `client_secret`. |
| 9 | As the project user, `GET /api/v2/configurations/oauth_apps/{project}?type=teams` and `?type=sharepoint`. | Teams: the app is not listed. SharePoint: the app is listed. |
| 10 | Same call with `?type=jira`. | 400 "Unsupported credential type: jira". |
| 11 | As admin, PUT with a changed endpoint and no secret. | 400 "Enter the client secret again when you change the endpoint". |
| 12 | DELETE the app, then DELETE it again. | 200, then 404 "OAuth app not found". |

---

## Expected Final State

No test app remains. Every invalid write was rejected by the server.
