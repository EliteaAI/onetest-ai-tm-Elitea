---
id: ELITEA-4443
title: "Stored Microsoft login with admin OAuth apps: Default app login, app change, secret rotation, editor save"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7262, issue:7149, stored-login, p1]
requirements: ["EliteaAI/elitea_issues#7262", "EliteaAI/elitea_issues#7149"]
---

# ELITEA-4443: Stored Microsoft login with admin OAuth apps: Default app login, app change, secret rotation, editor save

**Module:** toolkits-credentials · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify the credential-page stored login together with the admin-managed OAuth apps (#7149). A Default app credential's login is stored and used by schedules. A stored login belongs to the client it was made with, so an app change needs a new login, while a secret rotation does not. Also record whether an editor's ordinary save fails right after a Default app takes over a credential that has a stored login.

---

## Preconditions

- Admin Portal access (platform admin) to manage OAuth apps.
- A team project **P** with a **project admin** ADM and an **editor** ED.
- App **APP1** on Project 1 (public project), Teams on, **not** Default. A second app **APP2** on Project 1, Teams on, not Default.
- Microsoft account **MS-A**. A pipeline **PL** with a Teams tool, using the credential below.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ADM, create a Teams credential **C1** in P on the **Default app** tab with APP1 (name only). Save. Log in from the credential page as MS-A. | "Connected! The login is saved for scheduled runs."; `refresh_token` stored. |
| 2 | Run PL from a schedule. | Returns MS-A's teams with APP1's client. |
| 3 | As platform admin, **Replace** APP1's client secret with a new valid one. Run PL again. | Still works: same client ID, no new login needed. |
| 4 | As ADM, change C1's app to **APP2** and save. Run PL. | The old login (APP1's client) is not used: the run asks for a login. |
| 5 | As ADM, log in again on C1. Run PL. | Works with APP2. |
| 6 | As ADM, create a **Custom app** Teams credential **C2** (own Entra app), log in, and save. Then, as platform admin, make **APP1 Default**. | — |
| 7 | Run a schedule that uses C2. | C2 switches to APP1; its old login (own client) is not used, so the run asks for a login once. |
| 8 | **Record (suspected bug)**: right after step 6 (before C2 is used), as **ED** open C2, change only the display name, click Save. | Expected: saved. **Suspected:** 403 **"Only project admins can log in or out on a team credential"**, because the page no longer shows the stored login and the save looks like a login removal. Report if it happens. |
| 9 | As ADM, log in on C2. Run the schedule. | Works with APP1. |
| 10 | As platform admin, turn Default off on APP1. | C2 stays on APP1 (no automatic switch back); the stored login keeps working. |

---

## Expected Final State

C1 and C2 have stored logins made with their current app's client, and schedules work.

---

## Pass/Fail Criteria

**Pass:**
- Default app logins are stored and used by schedules.
- Secret rotation needs no new login; an app or client change needs exactly one.

**Fail:**
- A stored login made with one client is sent with another app's client.
- Secret rotation breaks the stored login.
- Step 8 returns 403 (file a bug).
