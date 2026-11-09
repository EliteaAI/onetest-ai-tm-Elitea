---
id: ELITEA-4289
title: "Admin Portal OAuth app: client secret is write-only, edit Save follows changes"
priority: critical
type: security
module: admin-portal/oauth-apps
status: ready
execution_type: manual
tags: [feat:admin-platform, nfr:security, int:oauth, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4289: Admin Portal OAuth app: client secret is write-only, edit Save follows changes

**Module:** admin-portal/oauth-apps · **Priority:** Critical · **Type:** Security

**Objective:** Verify that the client secret is never returned by the UI or the API once saved, that saving without Replace keeps it, that a changed endpoint needs the secret again, and that Save in the edit dialog is enabled only after a real change.

---

## Preconditions

- Admin user (Administration admin). Keycloak JWT for the API steps.
- App `OA_Test_4288` exists (ELITEA-4288) with a valid secret.
- A second valid secret for the same Entra app (for Replace).

---

## Test Data

| Field | Value |
|-------|-------|
| Admin list API | `GET /api/v2/admin/oauth_apps/administration` |
| Admin item API | `GET/PUT /api/v2/admin/oauth_apps/administration/{app_id}` |
| Second endpoint | `https://login.microsoftonline.com/organizations` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `OA_Test_4288` for edit. | Title "Edit Microsoft Entra ID app". The secret shows "Client secret: •••••••• (set)" with a **Replace** link. No secret value or input is shown. |
| 2 | Check Save. | **Disabled**. Test connection is enabled. |
| 3 | Change the Name, then change it back. | Save is enabled after the change and disabled again after revert. |
| 4 | Uncheck one Teams scope, then check it again. | Same: enabled, then disabled. |
| 5 | Change the name to `OA_Test_4289` and Save (no Replace). | Toast "App updated. Credentials that use it pick up the change." |
| 6 | Reopen and click **Test connection**. | "The client ID and secret are valid": the stored secret was kept. |
| 7 | Call the list API and the item API. | Each app has `client_secret_set: true`. There is **no** `client_secret` key, not even masked. The vault reference (`{{secret…}}`) is not returned. |
| 8 | In the dialog, change the endpoint to the second endpoint without Replace. | Endpoint field turns red: "Replace the client secret to use a new endpoint: the stored secret stays with the saved one." Save is disabled. |
| 9 | Send the same change by API: PUT with the new endpoint and no `client_secret`. | 400, field `client_secret`, "Enter the client secret again when you change the endpoint". |
| 10 | In the dialog, click **Replace**. | A password field appears with helper "The new value replaces the stored secret for every credential that uses this app." Save is enabled only after a value is entered. |
| 11 | Enter the second secret and Save. | Toast "App updated…". Test connection still succeeds. |
| 12 | Revert the endpoint to the tenant URL with Replace and the secret, and Save. | Saved. |
| 13 | PUT with `"provider": "other"` or a different provider value. | 400. The provider can't be changed. |
| 14 | Check the browser DevTools Network tab for all requests above. | No response body contains a secret value. |

---

## Postconditions

- Keep the app for later cases.
