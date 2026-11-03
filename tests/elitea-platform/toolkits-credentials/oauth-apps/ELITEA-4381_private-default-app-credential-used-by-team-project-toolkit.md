---
id: ELITEA-4381
title: "Private Default app credential used by a team project toolkit and agent"
priority: critical
type: functional
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:oauth, int:outlook, int:teams, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4381: Private Default app credential used by a team project toolkit and agent

**Module:** toolkits-credentials/oauth-apps · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a user's **private** Teams / Outlook credential in Default app mode can be selected in a team project toolkit, signs in with the admin app, and makes the team agent run with that user's own Microsoft account. Another team member gets their own private credential, not the first user's.

---

## Preconditions

- App **PUB** on **Project 1** (public project), **Default**, Teams and Outlook on. No other enabled app. Team project **pr_T** has no own app.
- Users **U1** and **U2**, editors in pr_T, each with a Microsoft account (mailbox + Teams).
- In pr_T, a toolkit **TK_OL** (Outlook) and an agent **AG_4381** using it. TK_OL refers to credential ID `ol_private_4381`.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential ID (U1 and U2) | `ol_private_4381` |
| Prompt | "Read my latest email and tell me its subject" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As U1, switch to the **Private** project → Credentials → New → Outlook. | No switcher, "Sign-in settings are managed by your administrator." (Project 1 Default applies in personal projects). |
| 2 | Set Display name and ID `ol_private_4381`, Save. | Saved with no warning. GET shows `oauth_app_id` = PUB, no secret. |
| 3 | Switch to **pr_T**, open TK_OL → Configuration. | The credential dropdown shows U1's **private** `ol_private_4381` and marks it as private. No missing-credential banner. |
| 4 | Open TK_OL sign-in from pr_T. | Scope is read-only with PUB's Outlook scopes. Sign in with U1's Microsoft account: success. The proxy request goes to `mcp_oauth_proxy/{pr_T}` with `oauth_app_id` = PUB and `credential_type: "outlook"`; no secret. |
| 5 | Run AG_4381 in pr_T with the prompt. | The tool runs with **U1's** mailbox. |
| 6 | As U2, repeat steps 1 – 2 in U2's private project, then open TK_OL in pr_T. | U2 sees **U2's own** private credential, not U1's. |
| 7 | U2 signs in and runs AG_4381. | The tool returns **U2's** mail. U1's next run still returns U1's mail. |
| 8 | As U2, delete the private credential and reopen TK_OL in pr_T. | The missing-credential banner is shown for U2 ("Create a credential" link). U1 is not affected. |
| 9 | Repeat steps 1 – 5 with **Teams** ("List my Teams chats"). | Same result. |

---

## Postconditions

- Delete U1's private credential, TK_OL and AG_4381.
