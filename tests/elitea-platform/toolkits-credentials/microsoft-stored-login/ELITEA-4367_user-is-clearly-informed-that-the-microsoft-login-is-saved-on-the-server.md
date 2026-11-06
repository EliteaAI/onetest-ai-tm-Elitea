---
id: ELITEA-4367
title: "[Parametrized] The user is clearly told that the Microsoft login is saved on the server, whose account it is, and that the whole project will use it"
priority: critical
type: security
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, int:sharepoint, issue:7262, issue:7037, stored-login, security, transparency, known-gap, p0]
requirements: ["EliteaAI/elitea_issues#7262", "EliteaAI/elitea_issues#7037"]
---

# ELITEA-4367: [Parametrized] The user is clearly told that the Microsoft login is saved on the server, whose account it is, and that the whole project will use it

**Module:** toolkits-credentials · **Priority:** Critical (P0) · **Type:** Security

**Objective:** Verify that a user who saves a Microsoft login understands what they are doing. Saving the login lets every project member, agent, pipeline and schedule act as that Microsoft account, after the browser is closed, until someone logs out. The user must be told:
1. that the login is **saved on the server**, not only in the browser,
2. **which Microsoft account** is saved,
3. that **everyone in the project** and all agents and schedules using the credential will **act as that account**,
4. how long it lasts, and how to remove it (Logout, or revoke at Microsoft).

The saved state must also stay visible later, not only in a toast.

**Known gap:** as of the #7262 fix, the only notice is the toast "Connected! The login is saved for scheduled runs.". There is no confirmation before saving, no account name, and no lasting notice. This case is expected to fail until a follow-up fix.

---

## Preconditions

- A team project **P** with admin **ADM** and editor **ED**.
- Microsoft test account **MS-A**.

---

## Test Data

| Variant | Where the login is made |
|---|---|
| Teams, credential page | Teams credential → Test connection |
| Outlook, toolkit bar | Outlook toolkit → Login |
| Dataverse, credential page | Dataverse credential → Test connection |
| SharePoint, toolkit bar | SharePoint toolkit → Login |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ADM, start the login for the variant. Before the Microsoft sign-in opens, or right after it, read what the page shows. | A clear notice or confirmation says the login will be **saved on the server** and **used by everyone in the project**, including agents and scheduled runs, until someone logs out. For a team credential, ADM must confirm before it is saved. |
| 2 | Complete the sign-in as MS-A. | The page names the saved account (for example **"Saved login: ms-a@contoso.com"**), not just **Connected!** or **Logout**. |
| 3 | Reload the page the next day, or open it in another browser. | The saved account name, and who saved it and when, are still shown. |
| 4 | As ED, open the same credential or toolkit. | ED sees that a saved login exists, which account it is, and that runs will act as that account. |
| 5 | As ADM, look for how to remove the login. | The page explains that **Logout** removes it for everyone, and that the user can also revoke it at Microsoft. |

---

## Expected Final State

Anyone who opens the credential or the toolkit can see that a Microsoft login is saved on the server, whose account it is, and that the whole project uses it.

---

## Pass/Fail Criteria

**Pass:**
- Steps 1–5 all show the information listed in the objective, for every variant.

**Fail:**
- The only sign of a saved login is a short toast, or **Logout** / **Connected!** without the account name.
- A team login is saved without the user confirming it will be shared with the project.
- Members cannot see whose account their runs act as.
