---
id: ELITEA-4358
title: "Logout in a second browser removes the saved Microsoft login, and the first browser keeps only its own session"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7262, stored-login, cross-browser, p0]
requirements: ["EliteaAI/elitea_issues#7262"]
---

# ELITEA-4358: Logout in a second browser removes the saved Microsoft login, and the first browser keeps only its own session

**Module:** toolkits-credentials · **Priority:** Critical (P0) · **Type:** Functional

**Objective:** Verify what happens when the login is saved from browser **A** and the user then opens the credential in browser **B**, which has no sign-in of its own:
- B still shows **Logout**, because a login is saved on the credential.
- Logout in B removes the saved login for scheduled runs and other users.
- A keeps working only with its own browser session, until that session ends or the page is reloaded.

---

## Preconditions

- A team project **P**. The tester is a **project admin**.
- A Teams credential **C** with no saved login, a Teams toolkit **T** using it, and an agent **AG** in P with T attached.
- A pipeline **PL** in P that calls a Teams tool through T.
- Two different browsers **A** and **B** (for example Chrome and Firefox), both logged in to ELITEA as the same tester.
- Microsoft test account **MS-A**.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In browser **A**, open C, click **Test connection** and sign in as MS-A. | Toast **"Connected! The login is saved for scheduled runs."** C shows **Logout**. |
| 2 | In browser **B**, open C. | C shows **Logout**, although B never signed in to Microsoft. |
| 3 | In browser **B**, open T. | The bar shows **Connected!**. |
| 4 | In browser **B**, open a chat with AG and ask it to list the user's joined teams. | The tool runs without a login prompt and returns MS-A's teams. B has no browser token, so this uses the saved login. |
| 5 | In browser **B**, open C, click **Logout** and confirm **Log out** in the dialog. | The dialog closes. C shows **Test connection**. `data.refresh_token` is missing from the credential GET response. |
| 6 | Run PL manually from browser **B**. | The Teams tool asks for an authorization ("log in" prompt) or fails with a sign-in error. It does not return data. |
| 7 | In browser **A**, without reloading, ask AG in a chat to list the user's joined teams, within 1 hour of step 1. | The tool works with A's own browser session. This is expected: logout in B does not reach A's browser. |
| 8 | In browser **A**, check C without reloading. | C may still show **Logout**, because the page has not been reloaded. |
| 9 | In browser **A**, reload C. | C shows **Logout** only while A's own browser session is still valid, and otherwise **Test connection**. It does not report a saved login. |
| 10 | Close browser A completely. Run PL again from browser B. | The tool asks for a login. No saved login is left anywhere. |

---

## Expected Final State

No login is saved on C. Only a browser session opened directly in browser A could still work, until it ends.

---

## Pass/Fail Criteria

**Pass:**
- B shows **Logout** in step 2 and its logout removes the saved login (steps 5–6).
- After step 10 nothing can use MS-A's account.

**Fail:**
- B shows **Test connection** in step 2 although a login is saved, so the user cannot log out from another browser.
- After the logout in B, a scheduled or manual pipeline run or another user can still use MS-A's account.
- After reloading A (step 9), the page reports a saved login that no longer exists.
