---
id: ELITEA-4302
title: "OAuth Apps — Create, Edit and Delete an App, Secret Never Returned"
priority: critical
type: regression
module: admin-portal/oauth-apps
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:admin-platform, nfr:security, int:oauth, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4302: OAuth Apps — Create, Edit and Delete an App, Secret Never Returned

**Module:** admin-portal/oauth-apps · **Priority:** critical · **Type:** regression

**Objective:** Regression of the OAuth app lifecycle in Admin Portal → Configuration → OAuth Apps: create with the required fields, the secret is write-only in the UI and the API, Save in edit follows real changes, and delete removes the app. Manual source: ELITEA-4288, ELITEA-4289, ELITEA-4292.

---

## Preconditions

- Logged in as an Administration admin.
- A team project exists to assign the app to.

---

## Test Data

| Field | Value |
|-------|-------|
| Name | `AT_OAuthApp_<timestamp>` |
| Client ID | any GUID |
| Client secret | any non-empty string |
| Endpoint | `https://login.microsoftonline.com/organizations` (default) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Configuration → OAuth Apps → **New Configuration for App**. | Dialog "New OAuth app". Provider "Microsoft Entra ID" is disabled. Save is disabled. |
| 2 | Fill Name, Client ID and Client secret. Leave Projects empty. | Save stays disabled. Projects helper "Required. The app applies only in the selected projects." |
| 3 | Select the team project and Save. | Toast "App created.". Row shows the name, chips Teams / Outlook / SharePoint, Projects "1 selected", Status "Enabled". |
| 4 | `GET /api/v2/admin/oauth_apps/administration`. | The app is listed with `client_secret_set: true` and **no** `client_secret` key. |
| 5 | Open the app for edit. | "Client secret: •••••••• (set)" with Replace. Save is **disabled**. |
| 6 | Change the Name, then revert it. | Save is enabled, then disabled again. |
| 7 | Change the Name and Save. | Toast "App updated. Credentials that use it pick up the change.". New name in the list. |
| 8 | Change the endpoint to `https://login.microsoftonline.com/common` without Replace. | Endpoint error "Replace the client secret to use a new endpoint…". Save disabled. Cancel. |
| 9 | Delete the app → Cancel, then Delete → confirm. | Cancel keeps it. Confirm → toast "App deleted.", row removed. |

---

## Expected Final State

The app is gone from the list and from the admin API. No API response contained the secret.
