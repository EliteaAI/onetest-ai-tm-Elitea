---
id: ELITEA-4473
title: "Author of team project agents and published agents is kept after the user's email changes in the IdP"
priority: high
type: functional
module: user-identity-sync
status: ready
execution_type: manual
tags: [feat:auth, feat:agents, feat:apps, int:oauth, issue:6184, email-change, p1]
requirements: ["EliteaAI/elitea_issues#6184"]
---

# ELITEA-4473: Author of team project agents and published agents is kept after the user's email changes in the IdP

**Module:** user-identity-sync · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify that agents the user created in a team project, and agents the user published, still show the user as the author after the email change, and that the user can still edit them.

---

## Preconditions

- Environment with the #6184 fix deployed (auth_oidc#3, auth_init#4, auth_core#22).
- A Keycloak realm admin who can edit users, and a second user **U2**.
- A Keycloak user **U** who has logged in to Elitea at least once **after** the deploy and has the **editor** role in team project **TP1**. Note U's user ID.
- **Setup (before the change):** as U, in TP1, create agent **TA1**. Create agent **PA1** and **publish** it. Note the author shown on TA1 and on PA1 in Agents Hub.
- **Email change:** log U out. In Keycloak, change U's **Email** (and **Username**, if editable) to a new value and save.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in to Elitea as U with the new credentials. Open TP1 → Agents → TA1. | The user ID is the same. The author of TA1 is U, shown with the current name or email. It is not the old email and not "unknown". |
| 2 | Edit TA1's instructions and save. | The change is saved. No permission error. |
| 3 | Run TA1 in a chat. | TA1 runs and returns a reply. |
| 4 | Open Agents Hub and find PA1. | PA1 is listed. The author is U, shown with the current name or email. |
| 5 | Run PA1 from Agents Hub. | PA1 runs and returns a reply. |
| 6 | As U2, open PA1 in Agents Hub. | The author is U, shown with the current name or email. |

---

## Expected Final State

TA1 and PA1 are still owned by U and show U as the author.

---

## Pass/Fail Criteria

**Pass:**
- The author is kept on TA1 and PA1, and U can still edit TA1.

**Fail:**
- The author shows the old email, is empty or unknown, or U can no longer edit TA1.
