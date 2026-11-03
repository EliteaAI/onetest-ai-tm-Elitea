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

**Objective:** Verify that a new login replaces the saved one right away. Runs must switch to the new account, even though the backend caches access tokens for up to about an hour.

---

## Preconditions

- A team project **P**. The tester is a **project admin**.
- A Teams credential **C**, a Teams toolkit **T** using it, and a pipeline **PL** calling a Teams tool through T.
- Two Microsoft accounts **MS-A** and **MS-B** with access to different teams.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On C, log in as MS-A. Close all other browser sessions of MS-A in ELITEA. | The login is saved. |
| 2 | Run PL. | PL returns MS-A's teams. The backend now has a cached access token for MS-A. |
| 3 | On C, click **Logout** → **Log out**, then log in again, this time as **MS-B**. | Toast **"Connected! The login is saved for scheduled runs."** |
| 4 | Within 5 minutes, close the browser and run PL from a schedule. | PL returns **MS-B's** teams. It does not use MS-A's cached token. |

---

## Expected Final State

Only MS-B's login is saved and used.

---

## Pass/Fail Criteria

**Pass:**
- Step 4 returns MS-B's data.

**Fail:**
- Any run after step 3 returns MS-A's data.
