---
id: ELITEA-4365
title: "SharePoint: a login on the credential page is either saved for scheduled runs, or the user is told it is kept in this browser only"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, int:sharepoint, issue:7262, stored-login, sharepoint, known-gap, p0]
requirements: ["EliteaAI/elitea_issues#7262"]
---

# ELITEA-4365: SharePoint: a login on the credential page is either saved for scheduled runs, or the user is told it is kept in this browser only

**Module:** toolkits-credentials · **Priority:** Critical (P0) · **Type:** Functional

**Objective:** Verify that a SharePoint login made on the **credential page** does not mislead the user. The #7262 fix saves credential-page logins for Dataverse, Outlook and Teams only; SharePoint saves a login only from its toolkit page bar. So a SharePoint login on the credential page shows **Logout** but, as of the #7262 fix, is kept in the current browser only, which is the same problem #7262 fixed for the other types.

One of these must be true:
- **A.** The SharePoint credential-page login is saved on the credential, like Teams (preferred), **or**
- **B.** The page clearly tells the user the login is kept in this browser only, and that it must be done from the toolkit page to work for scheduled runs and other users.

**Known gap:** as of the #7262 fix (EliteaUI #1347), neither A nor B is in place, so this case is expected to fail until a follow-up fix.

---

## Preconditions

- A team project **P**. The tester is a **project admin**.
- An Entra app with SharePoint delegated permissions (for example `Sites.Read.All`) and `offline_access`.
- A SharePoint site the test account **MS-A** can read.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In P, create a SharePoint credential **SC** with the app's client ID and secret, the discovery endpoint `https://login.microsoftonline.com/<tenant_id>` and the site URL. Save it. | SC is saved. |
| 2 | On SC, click **Test connection** and sign in as MS-A. | Either **A**: the toast **"Connected! The login is saved for scheduled runs."** appears; or **B**: a clear message says the login is kept in this browser only and must be done from the toolkit page to be used by scheduled runs and other users. |
| 3 | Check the SC GET response in DevTools. | For **A**: `data.refresh_token` is a `{{secret.…}}` reference. For **B**: it is not set, matching what the message said. |
| 4 | Look at SC's page after the sign-in. | If **B**, the page does not show a plain **Logout** that suggests a saved login. The state shown matches what is actually saved. |
| 5 | Create a SharePoint toolkit **ST** using SC, and a pipeline **SPL** that reads a file from the site through ST. Schedule SPL in 2–3 minutes and close the browser. | — |
| 6 | Check SPL's scheduled run. | For **A**: the run reads the file. For **B**: the run asks for a login, as the message warned. |

---

## Expected Final State

What the SharePoint credential page shows after a login matches what is saved, so the user is not misled.

---

## Pass/Fail Criteria

**Pass:**
- Outcome A or outcome B, with the page state, the saved data and the scheduled run all consistent.

**Fail:**
- The page shows **Logout** after a credential-page login, nothing is saved, no message explains it, and the scheduled run asks for a login. This is the #7262 bug, still present for SharePoint.
