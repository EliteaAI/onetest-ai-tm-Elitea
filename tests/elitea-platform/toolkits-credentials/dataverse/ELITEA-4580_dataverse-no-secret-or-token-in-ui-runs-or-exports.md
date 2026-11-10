---
id: ELITEA-4580
title: "Dataverse — no client secret, refresh token or access token in the UI, runs, logs or exports"
priority: critical
type: security
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8, nfr:security]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4580: Dataverse — no client secret, refresh token or access token in the UI, runs, logs or exports

**Module:** toolkits-credentials/dataverse · **Priority:** Critical · **Type:** Security

**Objective:** Verify the Dataverse secrets never leave the server: not in pages, API responses, run output, logs, exports or browser storage.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/mcp/callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**.
- A Dataverse toolkit **T** using C, all tools selected, and an agent **AG** with T.
- A login for MS-A saved on C (toolkit page → **Login**), unless the case says otherwise.
- A pipeline and a schedule that used T.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Credential page, toolkit page, credential list, toolkit GET (DevTools → Network). | No client secret, refresh token or access token value; only `{{secret.…}}` references. |
| 2 | After **Login** on T: DevTools → Application → Local / Session storage. | No Dataverse token left in the browser (it is removed after saving). |
| 3 | Chat run output, thinking steps, Run History, schedule run logs. | No token or secret. |
| 4 | Export the agent and the toolkit. | No secret, no refresh token; import asks for a credential. |
| 5 | API: predict call with a forged `dataverse_configuration` (another tenant / refresh_token) for C's uuid. | Ignored: the server uses C as saved. |
| 6 | API: predict with the uuid of a credential from another project. | No token injected; the tool asks for a login. |

---

## Expected Final State

No change.

---

## Pass/Fail Criteria

**Pass:**
- No secret or token value appears anywhere.

**Fail:**
- Any secret or token value is visible.
