---
id: ELITEA-4579
title: "Dataverse — schedule without a saved login: the risk check warns and the run waits for sign-in"
priority: high
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8, issue:7495]
requirements: ["EliteaAI/elitea_issues#7037", "EliteaAI/elitea_issues#7495"]
---

# ELITEA-4579: Dataverse — schedule without a saved login: the risk check warns and the run waits for sign-in

**Module:** toolkits-credentials/dataverse · **Priority:** High · **Type:** Functional

**Objective:** Verify that a schedule whose Dataverse credential has no saved login is flagged as needing a sign-in, and that with "Pause and ask me" the run waits for the owner instead of failing.

**Known:** [#7495](https://github.com/EliteaAI/elitea_issues/issues/7495): "Risk check: OK"; the run starts and fails at the first Dataverse call.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/app/mcp-auth-callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**. No login saved.
- A Dataverse toolkit **T** using C, all tools selected, and an agent **AG** with T.
- A private Dataverse credential (personal project) with a saved login, and a second toolkit using it.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a schedule for AG, approval rule **Pause and ask me**. | The form shows 'Toolkit "<T>" needs a personal sign-in; a scheduled run cannot sign in'. (Known bug #7495: no warning.) |
| 2 | **Run Now**. | The run waits for the owner ("Sign in or add the credentials before the run; otherwise the run waits for you."). (#7495: "Risk check: OK", then Failed.) |
| 3 | Log in on T, then approve / run again. | The run completes. |
| 4 | Schedule on an agent with the private-credential toolkit. | Warning that the toolkit runs with the owner's personal Dataverse credential; the run uses that login. |

---

## Expected Final State

Schedules deleted.

---

## Pass/Fail Criteria

**Pass:**
- A schedule without a login is flagged and waits.

**Fail:**
- The risk check says OK and the run fails (#7495).
