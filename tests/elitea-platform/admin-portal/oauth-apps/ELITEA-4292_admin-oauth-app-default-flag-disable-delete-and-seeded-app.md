---
id: ELITEA-4292
title: "Admin Portal OAuth app: Default flag, disable, delete and the seeded Elitea default app"
priority: high
type: functional
module: admin-portal/oauth-apps
status: ready
execution_type: manual
tags: [feat:admin-platform, int:oauth, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4292: Admin Portal OAuth app: Default flag, disable, delete and the seeded Elitea default app

**Module:** admin-portal/oauth-apps · **Priority:** High · **Type:** Functional

**Objective:** Verify how the Default flag behaves between two apps on Project 1, what a user's credential shows when its app is disabled, changed or deleted, that disable can be undone, that delete asks for confirmation, and that the seeded Elitea default app can be disabled but not deleted.

---

## Preconditions

- Admin user (Administration admin).
- **Project 1** is the public project: an app assigned to it applies in every project.
- Two apps, both assigned to **Project 1**, all 3 types on:
  - **APP_A**, Default **on**.
  - **APP_B**, Default **off**.
- User **U1** is an editor in a team project **pr_X**.
- Steps 13 – 15 only if the seeded "Elitea default app" is in the list.

---

## Test Data

| Field | Value |
|-------|-------|
| U1 credential | Outlook, name `OL_4292` |
| Throwaway app | `OA_Delete_4292`, Project 1 |

---

## Steps

### Part A: Default flag

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the list. | APP_A has chips "Enabled" and "Default". APP_B has "Enabled" only. |
| 2 | As U1 in pr_X, Credentials → New → Outlook. | **No switcher**: "Sign-in settings are managed by your administrator." (APP_A is Default). Save `OL_4292`. |
| 3 | As Admin, edit APP_B, switch **Default app** on, Save. Reload the list. | APP_B shows "Default". **APP_A has lost "Default"** without any warning: only one Default app per provider is kept, and the newest wins. Record it. The spec expects either this or a rejection with "… already has a default app: APP_A". |
| 4 | As U1, reopen `OL_4292` and run an agent that uses it. | The credential moves to **APP_B** on this use. U1 is asked to **sign in again** once. |
| 5 | As Admin, switch Default **off** on APP_B (no Default left). As U1, open New → Outlook. | Default app / Custom app switcher, with an **App** dropdown listing APP_A and APP_B. Two enabled apps with no Default give a dropdown. |
| 6 | Restore: APP_A Default on, APP_B Default off. | As in step 1. |

### Part B: Disable and change the app a credential uses

| # | Action | Expected Result |
|---|--------|-----------------|
| 7 | Switch Default off on APP_A (both apps non-default). As U1, edit `OL_4292`, pick **APP_B** in the App dropdown, Save. | Saved on APP_B. |
| 8 | As Admin, **disable** APP_B. As U1, open `OL_4292`. | The App field is empty and shows "APP_B was disabled by your administrator. Switch to Custom app." The credential **doesn't work** until the user acts. |
| 9 | Open the App dropdown. | Only **APP_A** is listed. Pick it and Save: the credential works again after one sign-in. |
| 10 | Re-enable APP_B. In the list, the row is no longer dimmed and the Status chip is "Enabled". | APP_B is offered again in the dropdown. |

### Part C: Delete and the seeded app

| # | Action | Expected Result |
|---|--------|-----------------|
| 11 | Create `OA_Delete_4292` and click its **delete** icon. | Dialog "Delete OAuth app": "Delete "OA_Delete_4292" and its client secret? Credentials that use it stop working and ask their owners to pick another app or switch to Custom app. To pause it instead, disable the app." Record whether it shows how many credentials use the app (spec: yes, not built). |
| 12 | Click **Cancel**, then delete again and confirm. | Cancel keeps the app. Confirm → toast "App deleted.", row gone, API GET by its id → 404 "OAuth app not found". |
| 13 | Delete the seeded **Elitea default app**. | Error: "The Elitea default app cannot be deleted. Disable it instead." App stays. |
| 14 | Edit the seeded app: check its Projects. | Projects = Project 1, Default on, Enabled on. |
| 15 | Disable the seeded app, then enable it again. | Both saves succeed. |

---

## Postconditions

- APP_A Default on, APP_B Default off, both enabled; the seeded app enabled. Delete `OL_4292`.
