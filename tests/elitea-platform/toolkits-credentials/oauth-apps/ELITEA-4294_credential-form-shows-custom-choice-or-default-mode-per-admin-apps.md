---
id: ELITEA-4294
title: "Teams, Outlook and SharePoint credential form shows Custom, Default/Custom or Default-only per admin apps"
priority: critical
type: functional
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:teams, int:outlook, int:sharepoint, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4294: Teams, Outlook and SharePoint credential form shows Custom, Default/Custom or Default-only per admin apps

**Module:** toolkits-credentials/oauth-apps · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the 4 form states of the Teams, Outlook and SharePoint credentials: no usable app, one non-default app, several non-default apps and a Default app. Check the API mode, the hidden Shared flag and the empty Custom tab.

---

## Preconditions

- Admin user and user **U1** (editor in team project **pr_A**). pr_A and Public have no apps at the start (disable the seeded app if present).
- Apps prepared but **disabled**: **A1** and **A2** for pr_A (not Default).

---

## Test Data

| Item | Value |
|------|-------|
| User API | `GET /api/v2/configurations/oauth_apps/{pr_A}?type=<teams|outlook|sharepoint>` |
| Types | Run steps 2 – 10 for **Teams**, **Outlook** and **SharePoint** |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As U1, call the user API for teams. | 200, `rows: []`, `mode: "custom"`. |
| 2 | Credentials → New → Teams. | **No switcher**. Custom app fields: Client ID, Client secret, OAuth discovery endpoint, Scopes, Auto refresh. Same as before the feature. |
| 3 | Check the Shared toggle. | **Not offered** for Teams / Outlook / SharePoint. (Open New → Jira: Shared is still offered there.) |
| 4 | As Admin, enable A1. As U1, reload New → Teams. | Default app / Custom app switcher. **Default app** tab is selected. No picker. "Sign-in settings are managed by your administrator." API: one row (A1), `mode: "choice"`. |
| 5 | On the Default app tab, look for client fields. | No Client ID, secret, endpoint, scopes or auto refresh fields. Only Name (and display name). |
| 6 | Switch to **Custom app**. | All Custom fields shown and **empty**; the endpoint is not prefilled with A1's endpoint. |
| 7 | As Admin, enable A2. As U1, reload New → Teams. | Switcher + app **picker** with "A1" and "A2". No app preselected. Save stays disabled until an app is picked. API: 2 rows, `mode: "choice"`. |
| 8 | As Admin, mark A1 **Default**. As U1, reload. | **No switcher**, no picker, only "Sign-in settings are managed by your administrator.". API: **only A1** row, `is_default: true`, `mode: "default"`. A2 is not returned. |
| 9 | Check every row of the API response. | Fields: id, name, provider, client_id, oauth_discovery_endpoint, is_default, scopes, auto_refresh_token. **No** client_secret. |
| 10 | Throttle the network (DevTools "Slow 3G") and open New → Teams. | The auth section is never blank: it waits, then shows the right mode. |
| 11 | Call the user API with `?type=jira`. | 400 "Unsupported credential type: jira". |
| 12 | SharePoint, Custom app tab: enter Client ID and secret, switch to **App-only** and back. | Client ID and secret are kept; both are required in each mode. |
| 13 | Open the Teams toolkit create form → credential field → create a new credential from there. | Same mode as on the Credentials page. |

---

## Postconditions

- Reset A1 Default off; disable A1 and A2.
