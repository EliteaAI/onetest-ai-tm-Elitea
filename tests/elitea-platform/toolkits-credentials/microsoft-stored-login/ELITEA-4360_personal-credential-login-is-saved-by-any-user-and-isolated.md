---
id: ELITEA-4360
title: "Any user can save a Microsoft login on their own personal credential, and nobody else can use it"
priority: high
type: security
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7262, stored-login, security, personal-project, p1]
requirements: ["EliteaAI/elitea_issues#7262"]
---

# ELITEA-4360: Any user can save a Microsoft login on their own personal credential, and nobody else can use it

**Module:** toolkits-credentials · **Priority:** High (P1) · **Type:** Security

**Objective:** Verify that the admin-only rule does not block users on their own **personal** credentials, and that a login saved there is not reachable by other users.

---

## Preconditions

- Users **U1** and **U2**, neither an admin of any shared team project.
- Microsoft test account **MS-A**.
- U1 and U2 share a team project **P** as members.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As U1, in U1's **personal** project, create a Teams credential **PC**. Click **Test connection** and sign in as MS-A. | Toast **"Connected! The login is saved for scheduled runs."** PC shows **Logout**, enabled. |
| 2 | As U1, schedule a personal pipeline that uses PC, and close the browser. | The scheduled run returns MS-A's Teams data. |
| 3 | As U1, check whether PC is listed among P's credentials, or can be picked in a toolkit in P. | PC is not listed and cannot be selected in P, unless U1 explicitly shared it. |
| 4 | As U2, try to open PC with `GET {{base_url}}/api/v2/configurations/configuration/<U1 personal project>/<PC id>`. | Refused (403 or 404). U2 does not get the credential or its `refresh_token` reference. |
| 5 | As U1, open PC and click **Logout** → **Log out**. | The login is removed. The scheduled pipeline asks for a login on its next run. |

---

## Expected Final State

PC has no saved login, and U2 never got access to it.

---

## Pass/Fail Criteria

**Pass:**
- U1 can log in and out on PC without being an admin.
- U2 cannot read or use PC.

**Fail:**
- U1 gets the admin-only error on a personal credential.
- U2 can read PC, its `refresh_token` reference, or run a toolkit with it.
