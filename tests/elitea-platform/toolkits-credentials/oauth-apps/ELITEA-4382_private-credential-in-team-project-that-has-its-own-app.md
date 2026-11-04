---
id: ELITEA-4382
title: "Private credential on a Project 1 app, used in a team project that has its own app"
priority: high
type: functional
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:oauth, int:outlook, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4382: Private credential on a Project 1 app, used in a team project that has its own app

**Module:** toolkits-credentials/oauth-apps · **Priority:** High · **Type:** Functional

**Objective:** Record how a private credential behaves when used in a team project whose own app replaces the Project 1 apps. The private credential's app is chosen by the **personal** project (Project 1 apps), but in the code the app check at runtime and at sign-in uses the **team** project. Spec R6 says the credential's own project must decide everywhere.

---

## Preconditions

- App **PUB** on **Project 1**, **Default**, Outlook on.
- App **TEAM** for team project **pr_T** only, **not** Default, Outlook on.
- User U1, editor in pr_T, with a Microsoft account.
- U1's **private** Outlook credential `ol_private_4382` in Default app mode (on PUB), and a toolkit **TK_OL** with an agent **AG_4382** in pr_T using it.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As U1, open the private credential in the **Private** project. | No switcher, PUB Default applies (no error). |
| 2 | Disable TEAM. In pr_T, sign in on TK_OL and run AG_4382. | Works with PUB. |
| 3 | Enable TEAM. In pr_T, open TK_OL → Configuration. | **Record** what the credential shows. Expected by spec R6: no error; the private credential stays on PUB. |
| 4 | Run AG_4382 in pr_T. | **Record.** Spec R6: runs with PUB. Code today: may fail with "The Microsoft Entra ID app selected for this credential is not available in this project. Switch to Custom app." because PUB is checked against pr_T, where TEAM replaces the Project 1 apps. If it fails, report a bug (R6). |
| 5 | Sign in again from TK_OL in pr_T. | **Record.** Spec: sign-in with PUB succeeds. Code today: may return 400 `app_unavailable` from `mcp_oauth_proxy/{pr_T}`. |
| 6 | As Admin, turn Default off on PUB. As U1, create a private **Custom app** Outlook credential (own client) and use it in pr_T. | Custom credentials don't depend on admin apps: works in pr_T. Turn Default on again on PUB. |
| 7 | Disable TEAM again. Run AG_4382. | Works with PUB again, no user action. |

---

## Postconditions

- Disable TEAM; delete test data.
