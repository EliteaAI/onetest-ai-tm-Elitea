---
id: ELITEA-4384
title: "Custom Outlook / Teams / SharePoint credential can be saved when all Entra ID apps are disabled (bug #7384)"
priority: critical
type: functional
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, int:outlook, int:teams, int:sharepoint, issue:7149, issue:7384, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7384", "EliteaAI/elitea_issues#7149"]
---

# ELITEA-4384: Custom Outlook / Teams / SharePoint credential can be saved when all Entra ID apps are disabled (bug #7384)

**Module:** toolkits-credentials/oauth-apps · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the fix of bug #7384: with every Entra ID app disabled in the Admin Portal, the credential form shows the plain Custom app form and its **Save** button becomes active once the required fields are filled, so the user can create the credential. Check team, private and Project 1 cases.

---

## Preconditions

- Admin user. All OAuth apps, including the seeded Elitea default app, are **disabled** (Admin Portal → Configuration → OAuth Apps).
- User U1, editor in team project **pr_T**, with a personal project.
- Client ID, secret and tenant of an Entra app registration that U1 owns (for the Custom fields).

---

## Test Data

| Field | Value |
|-------|-------|
| Display name / ID | `ol_custom_4384` |
| Client ID / secret | U1's own Entra app |
| OAuth discovery endpoint | `https://login.microsoftonline.com/organizations` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call `GET /api/v2/configurations/oauth_apps/{pr_T}?type=outlook`. | `rows: []`, `mode: "custom"`. |
| 2 | As U1 in pr_T, Credentials → New → **Outlook**. | Plain Custom app form, no Default app / Custom app switcher, no "No app is configured…" hint blocking the form. |
| 3 | Check Save before filling anything. | Disabled. |
| 4 | Fill Display name, ID, Client ID, Client secret, keep the endpoint and the preselected scopes. | **Save becomes active** (bug #7384: it stayed disabled). |
| 5 | Click Save. | Saved, back to the list, no warning. GET shows the own client_id, no `oauth_app_id`. |
| 6 | Repeat steps 2 – 5 for **Teams** and **SharePoint** (Delegated and App-only). | Save is active once required fields are filled; credential is saved. |
| 7 | Repeat steps 2 – 5 in U1's **private** project. | Same. |
| 8 | Clear one required field (e.g. Client secret). | Save becomes disabled again. Fill it: active again. |
| 9 | Open the saved credential and change only the name. | Save active, saved. |
| 10 | As Admin, enable a non-default app on Project 1. As U1, reopen `ol_custom_4384`. | Switcher with **Custom app** preselected and own values; leaving gives no warning. |
| 11 | Disable the app again. Create a new Outlook credential. | Same as step 4: Save is active. |
| 12 | Open New → Outlook while one app is enabled. As Admin, disable the last app. Reload the form. | The plain Custom form is shown and Save works after filling the required fields. |

---

## Postconditions

- Delete the test credentials; re-enable the apps that were enabled before.
