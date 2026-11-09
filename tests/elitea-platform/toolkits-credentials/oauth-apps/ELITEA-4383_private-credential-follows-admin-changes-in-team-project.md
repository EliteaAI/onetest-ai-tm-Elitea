---
id: ELITEA-4383
title: "Private credential used in a team project follows admin changes: Default adoption, disable, delete"
priority: high
type: functional
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:oauth, int:outlook, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4383: Private credential used in a team project follows admin changes: Default adoption, disable, delete

**Module:** toolkits-credentials/oauth-apps · **Priority:** High · **Type:** Functional

**Objective:** Verify that admin changes to Project 1 apps reach a **private** credential that is used by a team project toolkit: a new Default app is adopted (stored on the private credential, one new sign-in), a disabled app shows the reason in the team toolkit, and the user fixes it in the private project.

---

## Preconditions

- Apps **APP_1** and **APP_2** on **Project 1**, enabled, **not** Default. No apps for team project **pr_T**.
- U1 has a **private** Outlook credential `ol_private_4383` saved on **APP_2** (picked from the dropdown), signed in, used by toolkit **TK_OL** and agent **AG_4383** in pr_T.
- U1 also has an old **private Custom** Outlook credential `ol_custom_4383` (own client), used by a second toolkit **TK_OL2** in pr_T.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In pr_T, run AG_4383. | Works with APP_2. |
| 2 | As Admin, **disable** APP_2. In pr_T, open TK_OL. | The credential shows "APP_2 was disabled by your administrator. Switch to Custom app." (or the toolkit shows it can't use the credential). AG_4383 run fails with the same reason. |
| 3 | As U1, open the private credential in the **Private** project. | Same error. App dropdown lists only APP_1. Pick APP_1 and Save. |
| 4 | Back in pr_T, run AG_4383. | Asks U1 to sign in once (client changed), then works with APP_1. |
| 5 | As Admin, make APP_1 **Default**. In pr_T, run the agent with **TK_OL2** (private Custom credential). | The private Custom credential **adopts APP_1** (its own project, the personal one, has APP_1 as Default): U1 signs in once, then the run works with APP_1's client. |
| 6 | GET `ol_custom_4383` from the private project. | `oauth_app_id` = APP_1. The own client fields are kept in the DB. |
| 7 | Open `ol_custom_4383` in the private project. | No switcher, "Sign-in settings are managed by your administrator." |
| 8 | As Admin, delete APP_1. In pr_T, run both agents. | Both fail with "…no longer exists. Switch to Custom app." |
| 9 | Re-create a Project 1 app, U1 picks it on both private credentials. | Both work in pr_T after one sign-in each. |
| 10 | As another team member U2 (no private credentials), open TK_OL in pr_T. | U2 can't use U1's private credential: missing-credential banner. |

---

## Postconditions

- Delete test apps, credentials, toolkits and agent.
