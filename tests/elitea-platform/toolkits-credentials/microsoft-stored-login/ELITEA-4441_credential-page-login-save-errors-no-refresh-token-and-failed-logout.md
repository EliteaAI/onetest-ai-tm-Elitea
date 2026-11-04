---
id: ELITEA-4441
title: "Credential page login: no refresh token from Microsoft, and a Logout that fails on the server"
priority: medium
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7262, stored-login, p2, issue:7345, int:sharepoint]
requirements: ["EliteaAI/elitea_issues#7262", "EliteaAI/elitea_issues#7345"]
---

# ELITEA-4441: Credential page login: no refresh token from Microsoft, and a Logout that fails on the server

**Module:** toolkits-credentials · **Priority:** Medium (P2) · **Type:** Functional

**Objective:** Verify the two error paths of the credential-page login (#7262): when Microsoft returns no refresh token, nothing is stored and the user is told why; when removing the stored login fails on the server, the user is told, the dialog stays open and nothing is half-removed.

---

## Preconditions

- A team project **P**. The tester is a **project admin**.
- A Teams credential **C** (Custom app, own Entra app) and a Microsoft test account **MS-A**.
- For Part A, a way to get a sign-in without a refresh token: an Entra app or credential with **Auto refresh token (offline_access) off**.

**Variants:** run for **Teams** and again for a **SharePoint (Delegated)** credential (#7345). For SharePoint, also check that a schedule with the toolkit stays **blocked** by the risk review after Part A (no saved login).

---

## Steps

### Part A: no refresh token

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On C, switch **Auto refresh token** off (or use an app without `offline_access`). Save. | Saved. |
| 2 | Click **Test connection** and sign in as MS-A. | Toast **"Microsoft did not return a refresh token, so scheduled runs cannot use this login."** |
| 3 | Check the credential GET response. | `data.refresh_token` is not set. |
| 4 | Run a schedule that uses C. | The run asks for a login. |
| 5 | Switch Auto refresh token on, Save, log in again. | Toast **"Connected! The login is saved for scheduled runs."**; `refresh_token` stored. |

### Part B: Logout fails on the server

| # | Action | Expected Result |
|---|--------|-----------------|
| 6 | With the stored login from step 5, open DevTools → Network and block requests to `/api/v2/configurations/configuration/*` (request blocking), or switch the browser offline right before confirming. | — |
| 7 | On C, click **Logout** → **Log out**. | Error toast **"Could not remove the login from the credential."** (or the server's message). The dialog **stays open**. |
| 8 | Unblock requests and reload C. | C still shows **Logout**. GET: `refresh_token` still set. The browser token was not removed either. |
| 9 | Optional: as another project admin, demote the tester to editor while the dialog is open, then confirm **Log out**. | Error with the server's message **"Only project admins can log in or out on a team credential"**; stored login unchanged. |
| 10 | Click **Logout** → **Log out** normally. | Toast **"You have successfully logged out!"**; `refresh_token` removed; browser token removed. |

---

## Expected Final State

C has no stored login. No step left the credential in a state that differs from what the page showed.

---

## Pass/Fail Criteria

**Pass:**
- Part A: the refresh-token message is shown and nothing is stored.
- Part B: a failed removal keeps both the stored login and the browser token, and the page says so.

**Fail:**
- A login without a refresh token is reported as saved.
- A failed Logout removes the browser token, closes the dialog as if it worked, or leaves the page out of step with the stored data.
