---
id: ELITEA-4371
title: "The saved Microsoft login of a user who leaves the project or loses admin rights is flagged and can be removed"
priority: critical
type: security
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7262, issue:7037, stored-login, security, offboarding, known-gap, p0]
requirements: ["EliteaAI/elitea_issues#7262", "EliteaAI/elitea_issues#7037"]
---

# ELITEA-4371: The saved Microsoft login of a user who leaves the project or loses admin rights is flagged and can be removed

**Module:** toolkits-credentials · **Priority:** Critical (P0) · **Type:** Security

**Objective:** Verify what happens to a saved Microsoft login when the user who saved it is removed from the project, or stops being an admin. The project must not keep acting as a former member's Microsoft account without anyone knowing. Expected safe behaviour:
- the user is warned before leaving that their saved logins will stay or be removed, and
- remaining admins can see that a saved login belongs to a former member, and can remove it.

**Known gap:** as of the #7262 fix, no code removes or flags saved logins when a member leaves, and the saved login does not record who saved it. This case is expected to fail until a follow-up fix.

---

## Preconditions

- A team project **P** with admins **ADM1** and **ADM2**.
- A Teams credential **C** with a login saved by **ADM1** for Microsoft account **MS-A1**.
- A pipeline **PL** with a schedule that uses C.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ADM2, open C. | C shows that the login was saved by ADM1, with the account MS-A1 and the date. |
| 2 | As ADM2, change ADM1's role in P to editor. | A warning says ADM1 has a saved Microsoft login on C that the project will keep using, with an option to remove it. |
| 3 | As ADM2, remove ADM1 from P. | A warning says ADM1's saved Microsoft logins are still used by the project, with an option to remove them. ADM1 is told the same, if ADM1 leaves the project on their own. |
| 4 | Let PL run from the schedule after ADM1 is removed, without removing the login. | Record whether PL still runs as MS-A1. If it does, C must clearly show that the account belongs to a user no longer in the project. |
| 5 | As ADM2, on C, click **Logout** → **Log out**. | The saved login is removed. PL's next run asks for a login. |
| 6 | As ADM1, in a separate browser, check whether ADM1 can still see or remove the saved login on C after leaving. | ADM1 can no longer access C. ADM1 is told how to revoke the login at Microsoft (My Account → Sign out everywhere, or remove the app's consent). |

---

## Expected Final State

The project no longer uses MS-A1's account, and both ADM1 and ADM2 knew it was in use until it was removed.

---

## Pass/Fail Criteria

**Pass:**
- Steps 1–3 show who saved the login, and warn about it on role change and removal.
- ADM2 can remove the login in step 5.

**Fail:**
- After ADM1 leaves, PL keeps running as MS-A1, and nothing shows that the account belongs to a former member.
- ADM1 is not told that the project still uses their Microsoft account.
