---
id: ELITEA-4471
title: "Analytics show the user's usage from before and after the email change under the same user"
priority: high
type: functional
module: user-identity-sync
status: ready
execution_type: manual
tags: [feat:auth, feat:analytics, int:oauth, issue:6184, email-change, p1]
requirements: ["EliteaAI/elitea_issues#6184"]
---

# ELITEA-4471: Analytics show the user's usage from before and after the email change under the same user

**Module:** user-identity-sync · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify that the user's analytics from before the email change are kept, and new usage is added to the same user, not to a second user.

---

## Preconditions

- Environment with the #6184 fix deployed (auth_oidc#3, auth_init#4, auth_core#22).
- A Keycloak realm admin who can edit users.
- A Keycloak user **U** who has logged in to Elitea at least once **after** the deploy, is a member of a team project **TP1**, and has an agent **A1**. Note U's user ID.
- **Setup (before the change):** U sends messages in chats and runs A1 in the private project and in TP1. Wait until the usage appears in analytics. Record U's numbers (e.g. requests, tokens, cost) for each project and take screenshots.
- **Email change:** log U out. In Keycloak, change U's **Email** (and **Username**, if editable) to a new value and save.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in to Elitea as U with the new credentials. Open analytics for the private project. | The user ID is the same. The numbers from the setup are shown. |
| 2 | Open analytics for TP1. Filter by user, if a filter exists. | U is listed once, with the new email or name. The setup numbers are shown. There is no entry with the old email. |
| 3 | Send messages and run A1 again in both projects. Wait for analytics to update. | The new usage is added to U's numbers. |
| 4 | Check the user filter or user list in TP1 analytics again. | U is still listed once. The total is the setup numbers plus the new usage. |

---

## Expected Final State

All of U's usage, from before and after the change, is under one user in analytics.

---

## Pass/Fail Criteria

**Pass:**
- Old numbers are kept, and new usage is added to the same user.

**Fail:**
- Old usage is missing, or usage is split between an old-email user and a new-email user.
