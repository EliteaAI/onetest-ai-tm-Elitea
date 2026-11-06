---
id: ELITEA-4362
title: "A user's own browser Microsoft session is used instead of the saved team login"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7037, stored-login, p1]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4362: A user's own browser Microsoft session is used instead of the saved team login

**Module:** toolkits-credentials · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify that a run uses the saved login only when the browser sends no token for the credential. When a user is signed in to Microsoft in their own browser, their own account is used, not the admin's saved one.

---

## Preconditions

- A team project **P** with admin **ADM** and editor **ED**.
- A Teams credential **C** with a login saved by ADM for Microsoft account **MS-A**.
- A Teams toolkit **T** using C, and an agent **AG** in P with T attached.
- A second Microsoft account **MS-B** for ED, with access to different teams than MS-A.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ED, in a browser with no Microsoft sign-in, ask AG to list the user's joined teams. | MS-A's teams are returned (saved login). |
| 2 | As ED, in a chat with AG, trigger a Teams tool call that asks for authorization, and sign in as **MS-B** in the authorization popup. If no popup appears, sign in as MS-B from the toolkit's chat authorization flow. | ED's browser now has an MS-B session for this credential. |
| 3 | As ED, ask AG again to list the user's joined teams. | **MS-B's** teams are returned, not MS-A's. |
| 4 | As ED, close the browser, reopen it and ask the same in a new chat. | MS-A's teams are returned again, because the browser session ended. |

---

## Expected Final State

The saved login is used only when the user has no Microsoft session of their own.

---

## Pass/Fail Criteria

**Pass:**
- Step 3 returns MS-B's data and step 1 / step 4 return MS-A's data.

**Fail:**
- Step 3 returns MS-A's data although ED signed in as MS-B.
