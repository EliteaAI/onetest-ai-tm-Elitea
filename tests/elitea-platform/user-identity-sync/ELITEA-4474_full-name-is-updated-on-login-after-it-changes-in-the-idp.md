---
id: ELITEA-4474
title: "User's full name is updated on login after the first or last name changes in the IdP"
priority: high
type: functional
module: user-identity-sync
status: ready
execution_type: manual
tags: [feat:auth, feat:user-profile, int:oauth, issue:6184, issue:7335, name-change, p1]
requirements: ["EliteaAI/elitea_issues#6184", "EliteaAI/elitea_issues#7335"]
---

# ELITEA-4474: User's full name is updated on login after the first or last name changes in the IdP

**Module:** user-identity-sync · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify that when the user's first or last name changes in Keycloak, Elitea updates the full name on the next login, the same way it updates the email (#7335).

---

## Preconditions

- Environment with the #7335 fix deployed (auth_init#8).
- A Keycloak realm admin who can edit users.
- A Keycloak user **U** (First name `Poghos`, Last name `Poghosyan`) who has logged in to Elitea at least once and is a member of a team project **TP1**. Note U's user ID.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As U, open the profile page. | Full name is **Poghos Poghosyan**. |
| 2 | Log out. In Keycloak, change U's **Last name** to `Papikyan` and save. | Saved. |
| 3 | Log in to Elitea as U and open the profile page. | Full name is **Poghos Papikyan**. The user ID is the same. |
| 4 | As an admin, open Admin → Users and search for U. | One user, named **Poghos Papikyan**. |
| 5 | Open TP1 → Settings → Members. | U is shown as **Poghos Papikyan**. |
| 6 | Log out. In Keycloak, change U's **First name** to `Pogos` and the **Email** to a new value, and save. Log in again. | Profile shows **Pogos Papikyan** and the new email. The user ID is the same. |
| 7 | Log out and log in again without any change in Keycloak. | The name and email stay the same. |

---

## Expected Final State

U's full name and email in Elitea match the values in Keycloak, and there is one user record.

---

## Pass/Fail Criteria

**Pass:**
- The full name is updated on the first login after each Keycloak change, together with the email.

**Fail:**
- The old full name is still shown after login, or a new user is created.
