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

**Objective:** Verify that the admin-only rule does not block users on their own **personal** credentials, and that a login saved there is not reachable by other users. A run finds a stored login in the run's project and in the personal project of **the user the run executes as**, so a personal login is used only by runs as its owner, including the owner's schedules in a team project.

---

## Preconditions

- Users **U1** and **U2**, neither an admin of any shared team project.
- Microsoft test accounts **MS-A** (U1) and **MS-B** (U2).
- U1 and U2 share a team project **P** as members (editor or viewer).
- In P, a Teams toolkit **TP** that refers to credential ID `ms_private`, and an agent **AGP** using it. U1's personal credential in step 6 uses that ID.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As U1, in U1's **personal** project, create a Teams credential **PC**. Click **Test connection** and sign in as MS-A. | Toast **"Connected! The login is saved for scheduled runs."** PC shows **Logout**, enabled. |
| 2 | As U1, schedule a personal pipeline that uses PC, and close the browser. | The scheduled run returns MS-A's Teams data. |
| 3 | As U1, check whether PC is listed among P's credentials, or can be picked in a toolkit in P. | PC is not listed and cannot be selected in P, unless U1 explicitly shared it. |
| 4 | As U2, try to open PC with `GET {{base_url}}/api/v2/configurations/configuration/<U1 personal project>/<PC id>`. | Refused (403 or 404). U2 does not get the credential or its `refresh_token` reference. |
| 5 | As U1, open PC and click **Logout** → **Log out**. | The login is removed. The scheduled pipeline asks for a login on its next run. |
| 6 | As U1, create a personal Teams credential with ID `ms_private`, log in as MS-A from the credential page. In P, open TP. | TP uses U1's **personal** credential, marked private. No missing-credential banner. |
| 7 | As U1, add a schedule in P to a pipeline that uses TP. Close the browser. | The scheduled run (owner U1) returns MS-A's data from the stored login. |
| 8 | As U2 (no personal `ms_private`), chat with AGP in P. | U2 does **not** get MS-A's login: missing-credential banner or a login prompt. |
| 9 | As U2, create a personal `ms_private` **without** logging in, add a schedule in P to the same pipeline. | U2's schedule asks for a login / fails. It never falls back to U1's login. U1's schedule still works. |
| 10 | As U2, log in on U2's credential as MS-B. Run both schedules. | U1's run returns MS-A's data, U2's run returns MS-B's data. |
| 11 | Record: run the pipeline with a **system token** (a run with no person behind it). | The personal login is not found (no personal project for the run): login prompt / failure. |
| 12 | Record: if **governance is enforced** on the environment, check U1's scheduled run. | Mandate runs can't use a Microsoft sign-in credential: the run is refused. Note the environment's governance setting. |

---

## Expected Final State

PC has no saved login, and U2 never got access to it. Each user's schedules use only their own personal login.

---

## Pass/Fail Criteria

**Pass:**
- U1 can log in and out on PC without being an admin.
- U2 cannot read or use PC.

**Fail:**
- U1 gets the admin-only error on a personal credential.
- U2 can read PC, its `refresh_token` reference, or run a toolkit with it.
- U2's run or schedule uses U1's personal login.
