---
id: ELITEA-4363
title: "Logging in again with another Microsoft account replaces the saved login, and the old account is no longer used"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7037, stored-login, p1]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4363: Logging in again with another Microsoft account replaces the saved login, and the old account is no longer used

**Module:** toolkits-credentials · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify that a new login replaces the saved one right away. Runs must switch to the new account, even though the backend caches access tokens for up to about an hour (the cache key includes a hash of the refresh token, so a new login never reads the old cached token). Also record what happens when **two project admins** log in on the same team credential: there is one stored login per credential, and a browser token always wins over it.

---

## Preconditions

- A team project **P** with two **project admins**: **ADM1** and **ADM2**.
- A Teams credential **C**, a Teams toolkit **T** using it, an agent **AG** and a pipeline **PL** calling a Teams tool through T.
- Two Microsoft accounts **MS-A** (ADM1) and **MS-B** (ADM2) with access to different teams.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ADM1, on C, log in as MS-A. Close all other browser sessions of MS-A in ELITEA. | The login is saved. |
| 2 | Run PL. | PL returns MS-A's teams. The backend now has a cached access token for MS-A. |
| 3 | As ADM1, on C, click **Logout** → **Log out**, then log in again, this time as **MS-B**. | Toast **"Connected! The login is saved for scheduled runs."** |
| 4 | Within 5 minutes, close the browser and run PL from a schedule. | PL returns **MS-B's** teams. It does not use MS-A's cached token. |

### Part B: two admins on the same team credential

| # | Action | Expected Result |
|---|--------|-----------------|
| 5 | Reset: as ADM1, log out on C and log in as **MS-A**. Keep ADM1's browser open. | Login saved for MS-A. |
| 6 | As **ADM2** (another browser), open C. | C shows **Logout** (a stored login exists). **Record** whether anything shows *whose* account is saved. |
| 7 | As ADM2, look for **Login** while the stored login exists. **Record** whether ADM2 can log in without logging out first. If yes, log in as MS-B. | If allowed: the stored login is **replaced silently**; ADM1 gets no notice. |
| 8 | Otherwise, as ADM2, **Logout** → log in as **MS-B**. | Stored login = MS-B. |
| 9 | Run PL from a schedule. | Returns **MS-B's** teams. |
| 10 | As ADM1, in the still-open browser, ask AG to list joined teams. | Returns **MS-A's** teams: ADM1's browser token wins over the stored login. **Record**: two accounts are in use on one credential at the same time. |
| 11 | As ADM1, click **Logout** on C. | The stored login (MS-B) is removed for everyone, and ADM1's browser token too. PL's next run asks for a login. |

---

## Expected Final State

After step 4 only MS-B's login is saved and used. After step 11 no login is saved.

---

## Pass/Fail Criteria

**Pass:**
- Step 4 returns MS-B's data.

**Fail:**
- Any scheduled run after step 3 returns MS-A's data.
- A scheduled run after step 8 returns MS-A's data.

Steps 6, 7 and 10 are recorded for the product owner (whose login is saved, silent replace, two accounts at once).
