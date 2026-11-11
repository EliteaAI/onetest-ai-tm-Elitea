---
id: ELITEA-4469
title: "Private project and all its entities, secrets and tokens are kept after the user's email changes in the IdP"
priority: critical
type: functional
module: user-identity-sync
status: ready
execution_type: manual
tags: [feat:auth, feat:user-profile, int:oauth, issue:6184, email-change, p0]
requirements: ["EliteaAI/elitea_issues#6184"]
---

# ELITEA-4469: Private project and all its entities, secrets and tokens are kept after the user's email changes in the IdP

**Module:** user-identity-sync · **Priority:** Critical (P0) · **Type:** Functional

**Objective:** Verify that after the user's email changes in Keycloak, the user logs in to the same Elitea account and keeps the private project with all its entities, secrets and tokens.

---

## Preconditions

- Environment with the #6184 fix deployed (auth_oidc#3, auth_init#4, auth_core#22).
- A Keycloak realm admin who can edit users. To change the **username** too, turn on **Edit username** in Realm settings.
- A Keycloak user **U** (e.g. username `qa.rename.old`, email `qa.rename.old@epam.com`) who has logged in to Elitea at least once **after** the deploy. Note U's **user ID** from the profile page.
- **Setup (before the change):** in U's private project, create an agent **A1**, a pipeline **PL1**, a toolkit **T1**, a credential **C1**, a secret **S1** and a personal token **TK1**. Note the count of each entity type. Check that an API request with TK1 succeeds (any endpoint that needs auth, e.g. `GET {{base_url}}/api/v2/applications/applications/prompt_lib/<project_id>`).
- **Email change:** log U out. In Keycloak, change U's **Email** (and **Username**, if editable) to `qa.rename.new@epam.com` and save.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in to Elitea as U with the new credentials. Open the profile page. | Login works. The user ID is the same as before. The email is `qa.rename.new@epam.com`. |
| 2 | Open the private project. | The same private project opens. It is not a new, empty project. |
| 3 | Open Agents, Pipelines, Toolkits and Credentials. | A1, PL1, T1 and C1 are listed. The count of each entity type matches the setup. |
| 4 | Open Settings → Secrets. | S1 is listed. |
| 5 | Open Settings → Tokens. | TK1 is listed. |
| 6 | Send the same API request with TK1 as in the setup. | The request succeeds (no 401/403). |
| 7 | Open A1 and run it in a chat. | A1 opens, runs and returns a reply. |
| 8 | As an admin, open Admin → Users and search for both the old and the new email. | One user, with the new email. No user with `qa.rename.old@epam.com`. |

---

## Expected Final State

U has one Elitea account with the new email, and owns the private project and all its entities.

---

## Pass/Fail Criteria

**Pass:**
- Same user ID, all entities, secrets and tokens are present, and TK1 works.

**Fail:**
- A new user ID, an empty private project, missing entities, or TK1 is rejected.
- Two users (old and new email) in Admin → Users.
