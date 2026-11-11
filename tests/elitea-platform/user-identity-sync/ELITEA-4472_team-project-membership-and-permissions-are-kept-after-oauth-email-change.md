---
id: ELITEA-4472
title: "Team project membership and permissions are kept after the user's email changes in the IdP"
priority: critical
type: functional
module: user-identity-sync
status: ready
execution_type: manual
tags: [feat:auth, feat:user-profile, int:oauth, issue:6184, email-change, roles, p0]
requirements: ["EliteaAI/elitea_issues#6184"]
---

# ELITEA-4472: Team project membership and permissions are kept after the user's email changes in the IdP

**Module:** user-identity-sync · **Priority:** Critical (P0) · **Type:** Functional

**Objective:** Verify that after the user's email changes in Keycloak, the user still sees the team projects they were added to, with the same roles and permissions, and can be added to new projects by the new email.

---

## Preconditions

- Environment with the #6184 fix deployed (auth_oidc#3, auth_init#4, auth_core#22).
- A Keycloak realm admin who can edit users, and a project admin **PA** of team projects **TP1**, **TP2** and **TP3**.
- A Keycloak user **U** (e.g. email `qa.rename.old@epam.com`) who has logged in to Elitea at least once **after** the deploy. Note U's user ID.
- **Setup (before the change):** PA adds U to TP1 with the **editor** role and to TP2 with the **viewer** role. U logs in and opens both projects. U is not a member of TP3.
- **Email change:** log U out. In Keycloak, change U's **Email** (and **Username**, if editable) to `qa.rename.new@epam.com` and save.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in to Elitea as U with the new credentials. Open the project switcher. | The user ID is the same. TP1 and TP2 are listed. |
| 2 | As PA, open TP1 → Settings → Members. | U is listed with the **new** email and the **editor** role. The old email is not listed. |
| 3 | As PA, open TP2 → Settings → Members. | U is listed with the new email and the **viewer** role. |
| 4 | As U, in TP1, create an agent and save it. | The agent is created. |
| 5 | As U, in TP2, open an agent. | Edit, save and delete actions are not available, as for a viewer. |
| 6 | As PA, add a user to TP3 by typing `qa.rename.new@epam.com`. | U is found and added. As U, TP3 is listed in the project switcher. |
| 7 | As PA, try to add `qa.rename.old@epam.com` to TP3. | No user is found for the old email. A new user is not created. |

---

## Expected Final State

U is a member of TP1 (editor), TP2 (viewer) and TP3, shown with the new email.

---

## Pass/Fail Criteria

**Pass:**
- Both projects are listed with the same roles, permissions work as before, and U can be added by the new email.

**Fail:**
- A team project is missing, the role changed, members show the old email, or adding by the new email fails.
