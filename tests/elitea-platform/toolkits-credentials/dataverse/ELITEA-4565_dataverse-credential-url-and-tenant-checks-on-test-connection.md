---
id: ELITEA-4565
title: "Dataverse credential — URL and tenant ID checks, Test connection without a login"
priority: medium
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4565: Dataverse credential — URL and tenant ID checks, Test connection without a login

**Module:** toolkits-credentials/dataverse · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the URL and tenant checks of the Dataverse credential and what Test connection does when no login is saved.

**Known:** Tenant ID and Client ID formats are not checked on save; a wrong value only fails at the Microsoft sign-in (accepted, minor).

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/mcp/callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**. No login saved.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set URL to each value and click **Test connection**: `http://<org>.crm4.dynamics.com`, `https://<org>.crm4.dynamics.com/api/data/v9.2`, `https://<org>.crm4.dynamics.com:8443`, `https://dynamics.com`, `https://<org>.dynamics.com.evil.example`. | Each: "Dataverse URL must look like https://<org>.crm.dynamics.com". |
| 2 | Set URL with a trailing `/` and in upper case. | Accepted (normalised). |
| 3 | Set Tenant ID to `../x` or a value with spaces; Test connection. | "tenant_id must be a tenant GUID or domain name". |
| 4 | Set Tenant ID and Client ID to any short text (e.g. `abc`); save. | **Record**: saved without a check; the Microsoft sign-in later fails with an AADSTS error. |
| 5 | Restore valid values, save, click **Test connection**. | The Microsoft sign-in dialog opens (no saved login) instead of a plain failure. |

---

## Expected Final State

C has valid values and no saved login.

---

## Pass/Fail Criteria

**Pass:**
- Bad URLs and tenants are refused with the messages above; Test connection without a login starts the sign-in.

**Fail:**
- A non-Dataverse URL is accepted.
- Test connection without a login only reports a failure.
