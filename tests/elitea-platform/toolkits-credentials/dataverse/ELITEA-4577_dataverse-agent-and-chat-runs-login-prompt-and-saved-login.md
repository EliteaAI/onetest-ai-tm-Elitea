---
id: ELITEA-4577
title: "Dataverse — agent and chat runs: sign-in prompt without a login, saved login, runs as the saved account"
priority: critical
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8, issue:7497, issue:7494]
requirements: ["EliteaAI/elitea_issues#7037", "EliteaAI/elitea_issues#7497", "EliteaAI/elitea_issues#7494"]
---

# ELITEA-4577: Dataverse — agent and chat runs: sign-in prompt without a login, saved login, runs as the saved account

**Module:** toolkits-credentials/dataverse · **Priority:** Critical · **Type:** Functional

**Objective:** Verify agent and chat runs with the Dataverse toolkit: without a login the user is asked to sign in (popup), with a saved login the tools work without a browser login, and every user runs as the saved account.

**Known:** [#7497](https://github.com/EliteaAI/elitea_issues/issues/7497): without a login the tool returns "Tool execution error!" text and no sign-in popup.

**Known:** [#7494](https://github.com/EliteaAI/elitea_issues/issues/7494) (enhancement): no login state / Log in on the Dataverse card in the agent editor and in chat.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/app/mcp-auth-callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**. No login saved.
- A Dataverse toolkit **T** using C, all tools selected, and an agent **AG** with T.
- Project admin **ADM** and editor **ED**.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ADM, in AG's chat ask "who am I in Dataverse?". | The Microsoft sign-in popup opens (as for Outlook / SharePoint). (Known bug #7497: tool error text, agent tells the user to click Login.) |
| 2 | Agent editor and chat participants panel: look at the Dataverse toolkit. | **Record** whether a login state / Log in is shown (#7494). |
| 3 | Log in on T (toolkit page). Close other tabs. Ask again. | who_am_i returns MS-A; no popup. |
| 4 | As ED, the same chat question. | Returns MS-A (the saved login is used for everyone, known limit). |
| 5 | Logout on T; ask again. | The run asks for a login again; no stale cached token is used. |

---

## Expected Final State

C has a saved login.

---

## Pass/Fail Criteria

**Pass:**
- Without a login the user is asked to sign in; with a saved login it works without a browser login.

**Fail:**
- The run only returns error text (#7497).
- After logout the old login still works.
