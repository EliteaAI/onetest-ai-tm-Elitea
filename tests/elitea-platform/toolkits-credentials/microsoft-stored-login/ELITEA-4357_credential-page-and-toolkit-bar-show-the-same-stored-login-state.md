---
id: ELITEA-4357
title: "The credential page and the toolkit bar show the same stored Microsoft login state"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7262, stored-login, p1]
requirements: ["EliteaAI/elitea_issues#7262"]
---

# ELITEA-4357: The credential page and the toolkit bar show the same stored Microsoft login state

**Module:** toolkits-credentials · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify that a login saved from one place (the credential page or the toolkit page's **Connected / Login** bar) is shown as connected in the other. A logout from either place must also be reflected in both.

---

## Preconditions

- A team project **P**. The tester is a **project admin**.
- A Teams credential **C** in P with no saved login, set up as in ELITEA-4356 step 1.
- A Teams toolkit **T** in P that uses C.
- Microsoft test account **MS-A**.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open T. Check the login bar. | The bar shows **Not Connected** and a **Login** button. |
| 2 | Open C. Click **Test connection** and sign in as MS-A. | Toast **"Connected! The login is saved for scheduled runs."** The page shows **Logout**. |
| 3 | Open T again (reload the page). | The bar shows **Connected!** and a **Logout** button. |
| 4 | On T, click **Logout** and confirm. | Toast **"You have successfully logged out!"** The bar shows **Not Connected**. |
| 5 | Open C (reload the page). | The page shows **Test connection**, and no **Logout**. In DevTools, `data.refresh_token` is missing from the credential GET response. |
| 6 | On T, click **Login** and sign in as MS-A. | Toast **"Connected! The login is saved for scheduled runs."** The bar shows **Connected!**. |
| 7 | Open C (reload). Click **Logout**. | A dialog **"Log out of this credential?"** with a **Log out** button opens. |
| 8 | Click **Log out**. Open T (reload). | T's bar shows **Not Connected**. |

---

## Expected Final State

No login is saved on C, and both pages show it as not connected.

---

## Pass/Fail Criteria

**Pass:**
- After every login or logout, both pages show the same state once reloaded.

**Fail:**
- One page shows **Logout** / **Connected!** while the other shows not connected.
- A logout on one page leaves `data.refresh_token` on the credential.
