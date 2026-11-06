---
id: ELITEA-4442
title: "Two admins with their own personal credentials on one team toolkit keep separate stored logins"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7262, stored-login, personal-project, p1]
requirements: ["EliteaAI/elitea_issues#7262"]
---

# ELITEA-4442: Two admins with their own personal credentials on one team toolkit keep separate stored logins

**Module:** toolkits-credentials · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify that two project admins who each use their **own personal** credential with the same team toolkit keep separate stored logins. A re-login or Logout by one never affects the other, and each schedule runs as its owner's Microsoft account.

---

## Preconditions

- A team project **P** with two **project admins**: **ADM1** and **ADM2**.
- Microsoft accounts **MS-A** (ADM1) and **MS-B** (ADM2) with access to different teams.
- In P, a Teams toolkit **T** that refers to credential ID `ms_private`, and a pipeline **PL** calling a Teams tool through T.
- No team credential with ID `ms_private` in P.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ADM1, in ADM1's personal project, create a Teams credential `ms_private`, log in as MS-A from the credential page. | "Connected! The login is saved for scheduled runs." |
| 2 | As ADM2, do the same in ADM2's personal project with MS-B. | Same. |
| 3 | As ADM1 and as ADM2, open T in P. | Each sees **their own** personal credential, marked private. |
| 4 | ADM1 and ADM2 each add a schedule in P to PL (or each owns a copy of PL). Close the browsers. | ADM1's run returns MS-A's teams; ADM2's run returns MS-B's teams. |
| 5 | As ADM1, log out and log in again on the personal credential, this time as **MS-C** (or MS-A again). | Only ADM1's credential changes. |
| 6 | Run both schedules. | ADM1's run uses the new login; ADM2's still returns MS-B's teams. |
| 7 | As ADM1, **Logout** on the personal credential. Run both schedules. | ADM1's run asks for a login; ADM2's run still works. |
| 8 | As ADM1, try to read or change ADM2's personal credential: `GET` / `PUT {{base_url}}/api/v2/configurations/configuration/<ADM2 personal project>/<id>`. | Refused (403 or 404). |
| 9 | As ADM1 in P, list credentials. | ADM2's personal credential is not listed; being a project admin gives no access to it. |

---

## Expected Final State

ADM1 has no stored login; ADM2's stored login and schedule are unchanged.

---

## Pass/Fail Criteria

**Pass:**
- Each schedule runs only with its owner's login, before and after the other admin's re-login and Logout.

**Fail:**
- One admin's login, re-login or Logout changes the other's stored login or runs.
- A project admin can read or change another user's personal credential.
