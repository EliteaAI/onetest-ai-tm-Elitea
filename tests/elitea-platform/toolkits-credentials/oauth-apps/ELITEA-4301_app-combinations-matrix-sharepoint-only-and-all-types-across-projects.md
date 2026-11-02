---
id: ELITEA-4301
title: "OAuth app combinations on Project 1: SharePoint-only app and all-types app, with and without Default"
priority: critical
type: functional
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, feat:admin-platform, int:teams, int:outlook, int:sharepoint, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4301: OAuth app combinations on Project 1: SharePoint-only app and all-types app, with and without Default

**Module:** toolkits-credentials/oauth-apps · **Priority:** Critical · **Type:** Functional

**Objective:** Verify what the Teams, Outlook and SharePoint credential forms show for each combination of two admin apps assigned to **Project 1** (the public project, so they apply in every project): one that supports only SharePoint and one that supports all 3 types, with and without the Default flag.

---

## Preconditions

- Admin user (Administration admin).
- User **U1** is an editor in a team project **pr_X** and has a personal project.
- No other enabled OAuth app (disable the seeded Elitea default app if it is listed).
- Two apps, both assigned to **Project 1**, created disabled and changed between combinations:
  - **APP_SP**: only **SharePoint** switched on (Teams and Outlook off).
  - **APP_ALL**: **Teams, Outlook and SharePoint** switched on.

---

## How to read the table

| Form state | What U1 sees |
|---|---|
| **Custom** | Plain Custom app form, no Default app / Custom app switcher |
| **Switcher** | Default app / Custom app switcher, one app used, no App dropdown |
| **Dropdown** | Switcher + App dropdown listing the apps |
| **Default** | No switcher: "Sign-in settings are managed by your administrator." |

Check each cell in **pr_X** and in the **personal** project (results must be the same) and with `GET /api/v2/configurations/oauth_apps/{project_id}?type=<type>` (`mode`: Custom = `custom`, Switcher / Dropdown = `choice`, Default = `default`).

---

## Test Data

| # | APP_SP | APP_ALL | Teams | Outlook | SharePoint |
|---|---|---|---|---|---|
| C1 | enabled | disabled | Custom | Custom | Switcher (APP_SP) |
| C2 | disabled | enabled | Switcher (APP_ALL) | Switcher (APP_ALL) | Switcher (APP_ALL) |
| C3 | enabled | enabled | Switcher (APP_ALL) | Switcher (APP_ALL) | **Dropdown** (APP_SP, APP_ALL) |
| C4 | enabled, **Default** | enabled | Switcher (APP_ALL) | Switcher (APP_ALL) | Default (APP_SP) |
| C5 | enabled | enabled, **Default** | Default (APP_ALL) | Default (APP_ALL) | Default (APP_ALL) |
| C6 | enabled, Default | enabled, then set **Default** | see step 7 | see step 7 | see step 7 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Admin, open the list. | Credentials chips: APP_SP = SharePoint, APP_ALL = Teams, Outlook, SharePoint. Projects "1 selected" for both. |
| 2 | **C1**. As U1, open Credentials → New → Teams, Outlook, SharePoint in pr_X and in the personal project. | As in the table. Teams and Outlook show the plain Custom form: APP_SP doesn't serve them. |
| 3 | **C2**. | As in the table. |
| 4 | **C3**. | As in the table. SharePoint has an App dropdown with APP_SP and APP_ALL and nothing preselected. Save stays disabled until an app is picked. |
| 5 | **C4**. | As in the table. Teams and Outlook keep the switcher: APP_SP is Default, but it doesn't serve them. For SharePoint, APP_ALL is not offered and the API returns only APP_SP. |
| 6 | **C5**. | As in the table. APP_SP is not offered anywhere; the API returns only APP_ALL. |
| 7 | **C6**: start from C4 (APP_SP Default). Edit APP_ALL, switch Default on, Save. Reload the list. | **Record.** Today APP_SP **silently loses Default** (one Default per provider, newest wins), so the result is the same as C5. Spec expectation: Save is rejected ("… already has a default app: APP_SP"). Either way the admin gets no warning that the other app changed. |
| 8 | **C3** + switch **SharePoint off** on APP_ALL. | SharePoint: Switcher with APP_SP only (no dropdown). Teams and Outlook: still Switcher (APP_ALL). |
| 9 | **C4** + **disable** APP_SP. | SharePoint becomes Switcher (APP_ALL). Teams and Outlook unchanged. |
| 10 | **C3**: U1 saves a SharePoint credential on APP_SP. Admin disables APP_SP. U1 opens it. | "APP_SP was disabled by your administrator. Switch to Custom app." The dropdown now lists only APP_ALL. U1 picks APP_ALL and saves; the credential works after one sign-in. |
| 11 | For every step, compare the form with the API `mode` and rows. | They always match. The API never returns a Default and a non-default app together. No `client_secret` in the rows. |

---

## Postconditions

- Disable or delete APP_SP and APP_ALL; re-enable the seeded app if it was disabled.
