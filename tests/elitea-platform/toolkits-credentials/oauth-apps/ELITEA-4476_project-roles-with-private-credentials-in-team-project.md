---
id: ELITEA-4476
title: "Project roles with private Default app credentials used in a team project"
priority: high
type: functional
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, nfr:security, int:oauth, int:outlook, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4476: Project roles with private Default app credentials used in a team project

**Module:** toolkits-credentials/oauth-apps · **Priority:** High · **Type:** Functional

**Objective:** Verify that viewer, editor and admin of a team project can each use **their own private** Default app credential with a team toolkit, sign in on it (they own their personal project, so the team-credential sign-in rule doesn't block them), and never see or use another member's private credential.

---

## Preconditions

- App **PUB** on **Project 1**, **Default**, Outlook on. No app for team project **pr_R**.
- Users **V** (viewer), **E** (editor), **A** (admin) in pr_R, each with a Microsoft account.
- In pr_R: an Outlook toolkit **TK_OL** referring to credential ID `ol_private_4476`, and agent **AG_4476** using it (created by A).

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As **V**, in the **Private** project create an Outlook credential `ol_private_4476` (name only). | Saved: V is the owner of the personal project. |
| 2 | As V, sign in on it (from the private project). | Allowed and stored: the team-credential rule doesn't apply to an own personal credential. |
| 3 | As V, open TK_OL in pr_R. | V's private credential is used and marked private. V can't edit the toolkit (viewer). |
| 4 | As V, chat with AG_4476 in pr_R (if viewers can chat). | Runs with **V's** mailbox. |
| 5 | As **E**, repeat steps 1 – 4 with E's private credential. | Same, with E's mailbox. E can also edit TK_OL. |
| 6 | As **A**, repeat steps 1 – 4. | Same, with A's mailbox. |
| 7 | As E, change TK_OL's credential to a **team** credential and Save. | Allowed (editor). Then E's sign-in on that team credential → 403 "Only project admins can log in or out on a team credential". |
| 8 | Revert TK_OL to `ol_private_4476`. As V, E and A, list Credentials in pr_R. | None of them sees another member's private credential. |
| 9 | As E, call the user API `GET /configurations/oauth_apps/{V's personal project}?type=outlook`. | 403/404: no access to another user's personal project. |
| 10 | As V, PUT E's private credential via API (`/configurations/configuration/{E's personal project}/{id}`). | 403/404. E's credential and stored login are unchanged. |

---

## Postconditions

- Delete the private credentials, TK_OL and AG_4476.
