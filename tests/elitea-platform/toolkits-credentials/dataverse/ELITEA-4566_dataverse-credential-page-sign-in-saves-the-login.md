---
id: ELITEA-4566
title: "Dataverse credential page — sign-in from Test connection saves the login, no login loop"
priority: high
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8, issue:7492, issue:7496, issue:7493]
requirements: ["EliteaAI/elitea_issues#7037", "EliteaAI/elitea_issues#7492", "EliteaAI/elitea_issues#7496", "EliteaAI/elitea_issues#7493"]
---

# ELITEA-4566: Dataverse credential page — sign-in from Test connection saves the login, no login loop

**Module:** toolkits-credentials/dataverse · **Priority:** High · **Type:** Functional

**Objective:** Verify that a Microsoft sign-in started from the Dataverse credential page is saved on the credential and does not reopen again and again. Also check the dialog wording and the missing Login / Logout button.

**Known:** [#7492](https://github.com/EliteaAI/elitea_issues/issues/7492): "Microsoft did not return a refresh token…" and the sign-in reopens in a loop.

**Known:** [#7496](https://github.com/EliteaAI/elitea_issues/issues/7496): the dialog says "This MCP server requires OAuth authorization…".

**Known:** [#7493](https://github.com/EliteaAI/elitea_issues/issues/7493) (enhancement): no Login / Logout button on the Dataverse credential page.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/mcp/callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**. No login saved. Tester is project admin.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open C → **Test connection**. | The sign-in dialog opens: server `https://login.microsoftonline.com/<tenant>`, scope `<url>/user_impersonation offline_access`. Wording is about a Microsoft sign-in, not an MCP server (#7496). |
| 2 | **Authorize** and sign in as MS-A. | Toast "Connected! The login is saved for scheduled runs."; the connection test then passes. (Known bug #7492: "Microsoft did not return a refresh token…".) |
| 3 | Watch the page for 30 s. | The sign-in does not open again. (#7492: it reopens.) |
| 4 | API: GET C. | `refresh_token` is set (vault reference). |
| 5 | Open toolkit T (using C). | The Login bar shows **Connected!**. |
| 6 | Look for Login / Logout on the credential page. | **Record**: only Test connection exists (#7493). |

---

## Expected Final State

C has a saved login for MS-A.

---

## Pass/Fail Criteria

**Pass:**
- The sign-in from the credential page is saved once, without a loop.

**Fail:**
- The login is not saved, or the sign-in keeps reopening (#7492).
