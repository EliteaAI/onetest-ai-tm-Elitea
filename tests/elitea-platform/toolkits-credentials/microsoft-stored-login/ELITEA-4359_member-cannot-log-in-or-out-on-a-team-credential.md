---
id: ELITEA-4359
title: "A project member cannot log in or out on a team Microsoft credential, from the UI or the API"
priority: critical
type: security
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7262, stored-login, security, roles, p0, issue:7345, int:sharepoint]
requirements: ["EliteaAI/elitea_issues#7262", "EliteaAI/elitea_issues#7345"]
---

# ELITEA-4359: A project member cannot log in or out on a team Microsoft credential, from the UI or the API

**Module:** toolkits-credentials · **Priority:** Critical (P0) · **Type:** Security

**Objective:** Verify that only project admins can save, replace or remove the Microsoft login on a team credential. Members (editors and viewers) see the controls disabled, and the server refuses the change even when the UI is bypassed.

---

## Preconditions

- A team project **P** with an admin **ADM** and a member **ED** with the **editor** role.
- A Teams credential **C** in P with a login saved by ADM (as in ELITEA-4356 steps 1–2).
- A Teams credential **C2** in P with no saved login.
- A Teams toolkit **T** using C.

**Variants:** run the steps for **Teams** and again for **SharePoint (Delegated)** credentials (#7345: SharePoint credential-page logins follow the same rule). For SharePoint, T is a SharePoint toolkit; its page has SharePoint's own login bar.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ED, open C. | **Logout** is shown but disabled. Hovering it shows **"Login managed by a project admin"**. |
| 2 | As ED, open C2. Hover the disabled login control. | The hint **"Not connected, ask a project admin to log in"** is shown. |
| 3 | As ED, on C2, click **Test connection**. | No Microsoft sign-in window opens. The page reports that a project admin must log in. |
| 4 | As ED, open T. | The bar's button is disabled, with the same admin hint. |
| 5 | As ED, open DevTools → Network on C. Copy the credential's `data` from the GET response. Send `PUT {{base_url}}/api/v2/configurations/configuration/<project>/<C id>` with the same `data` but **without** `refresh_token`. | The request is refused with **403** and the error **"Only project admins can log in or out on a team credential"**. The saved login is still there. |
| 6 | As ED, send the same PUT with `refresh_token` set to any made-up value. | **403**, same error. The saved login is unchanged. |
| 7 | As ED, on C2, send a PUT that adds `refresh_token`. | **403**, same error. C2 still has no saved login. |
| 8 | As ED, create a new Teams credential in P through `POST /api/v2/configurations/configurations/<project>` with a `refresh_token` in `data`. | The request is refused with **403** and the same error. |
| 9 | As ADM, open C. | **Logout** is enabled. The saved login from the preconditions is unchanged. |

---

## Expected Final State

Only ADM's original login is saved on C, and C2 has none.

---

## Pass/Fail Criteria

**Pass:**
- All member attempts in steps 3 and 5–8 are refused, and nothing changes on the server.

**Fail:**
- A member can open a Microsoft sign-in from Test connection on a team credential.
- Any member PUT or POST sets, replaces or removes `refresh_token`.
