---
id: ELITEA-4304
title: "OAuth Apps — Credential Form Shows Custom, Switcher, Dropdown or Default Only"
priority: critical
type: regression
module: toolkits-credentials/oauth-apps
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:credentials, int:teams, int:outlook, int:sharepoint, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4304: OAuth Apps — Credential Form Shows Custom, Switcher, Dropdown or Default Only

**Module:** toolkits-credentials/oauth-apps · **Priority:** critical · **Type:** regression

**Objective:** Regression of the 4 Teams / Outlook / SharePoint credential form states driven by admin OAuth apps on Project 1. Apps are set up through the admin API, and the form is checked in the UI. Manual source: ELITEA-4294, ELITEA-4301.

---

## Preconditions

- Admin JWT for setup. A project user logged in to the UI.
- No other enabled OAuth app (the seeded app is disabled).
- Two apps on **Project 1** (the public project), created by API and disabled: **APP_1** and **APP_2**, all 3 types.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Credentials → New → Outlook. | No Default app / Custom app switcher. Custom fields: Client ID, Client secret, OAuth discovery endpoint, Scopes. |
| 2 | Look for the Shared toggle. | Not offered. |
| 3 | Enable APP_1 (API). Reload New → Outlook. | Switcher, **Default app** selected, no App dropdown, "Sign-in settings are managed by your administrator." |
| 4 | Click **Custom app**. | Custom fields are shown and empty. |
| 5 | Enable APP_2 (API). Reload. | Switcher + **App** dropdown with APP_1 and APP_2. Nothing preselected. Save is disabled until a name and an app are set. |
| 6 | Set APP_1 as Default (API). Reload. | No switcher, no dropdown, only "Sign-in settings are managed by your administrator." |
| 7 | Repeat the step 6 check for Teams and SharePoint. | Same result. |

---

## Expected Final State

The form state always matches `mode` (custom / choice / default) from `GET /api/v2/configurations/oauth_apps/{project}?type=`.

## Teardown

Delete APP_1 and APP_2. Re-enable the seeded app if it was disabled.
