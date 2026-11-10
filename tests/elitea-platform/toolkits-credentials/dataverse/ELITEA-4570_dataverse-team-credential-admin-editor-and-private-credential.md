---
id: ELITEA-4570
title: "Dataverse — who can log in and out: project admin, editor, private credential, two admins"
priority: high
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4570: Dataverse — who can log in and out: project admin, editor, private credential, two admins

**Module:** toolkits-credentials/dataverse · **Priority:** High · **Type:** Functional

**Objective:** Verify that only project admins can log in or out on a team Dataverse credential, that anyone can on their own private credential, and that a second admin's login replaces the first.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/app/mcp-auth-callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**.
- A Dataverse toolkit **T** using C, all tools selected, and an agent **AG** with T.
- Users: project admin **ADM**, editor **ED** of P; a second admin **ADM2** with Microsoft account **MS-B**.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ED, open T (no login on C). | Bar shows the state; **Login** disabled with tooltip "Only project admins can log in or out on a team credential". |
| 2 | As ED, API PUT C with a `refresh_token` value; then an unrelated change (label). | 403 "Only project admins can log in or out on a team credential"; the label change is 200. |
| 3 | As ADM, log in as MS-A. | Saved; ED now sees **Connected!** but **Logout** is disabled for ED. |
| 4 | As ED, run who_am_i in an agent with T. | UserId of **MS-A** (everyone runs as the saved login, known limit). |
| 5 | As ED, create a private Dataverse credential in the personal project, a toolkit with it, and log in. | Allowed; saved on the private credential. |
| 6 | As ADM2, log in on C as MS-B. | The saved login is replaced with no prompt; who_am_i returns MS-B. **Record** that nothing shows who logged in. |

---

## Expected Final State

C has one saved login; ED's private credential deleted.

---

## Pass/Fail Criteria

**Pass:**
- Only admins change a team login; private credentials are managed by their owner.

**Fail:**
- An editor can save or remove a team login.
