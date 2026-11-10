---
id: ELITEA-4564
title: "Dataverse credential — create: form fields, required fields, secret storage, private and team"
priority: high
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4564: Dataverse credential — create: form fields, required fields, secret storage, private and team

**Module:** toolkits-credentials/dataverse · **Priority:** High · **Type:** Functional

**Objective:** Verify the Dataverse (OneCRM) credential type: it can be found, its form has URL, Tenant ID, Client ID and Client secret (no refresh token field), required fields are enforced, the secret is stored in the vault, and it can be private or team.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/app/mcp-auth-callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- Team project **P** (tester is project admin) and the tester's personal project.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Credentials → **+ Create** → search `dataverse`, then `onecrm`, `crm`, `dynamics`, `microsoft`. | **Dataverse (OneCRM)** is found by each term, with the Dataverse icon. |
| 2 | Open it. | Fields **Url**, **Tenant Id**, **Client Id**, **Client Secret** (masked), all required. No Refresh token field. |
| 3 | Clear each required field in turn and try to save. | Save is refused; the empty field is marked required. |
| 4 | Fill all fields with the test app values and save. | Saved; the credential opens; the secret is shown masked. |
| 5 | API: `GET /api/v2/configurations/configuration/prompt_lib/{P}/{id}` and the credential list. | `client_secret` is a vault reference (`{{secret.…}}`), never the value. |
| 6 | Create the same credential in the personal project (private). | Saved; it is offered in a team-project toolkit as a private credential. |
| 7 | Delete a credential that a toolkit uses, then open the toolkit. | The toolkit shows that its credential is missing. |

---

## Expected Final State

One team and one private Dataverse credential exist (delete the extra ones).

---

## Pass/Fail Criteria

**Pass:**
- All steps behave as expected.

**Fail:**
- A refresh token field is visible or editable.
- The secret value is returned by any API or shown in the UI.
