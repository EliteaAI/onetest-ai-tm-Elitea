---
id: ELITEA-4361
title: "A Microsoft login made while the credential has unsaved edits is not saved"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7262, stored-login, p1, issue:7345, int:sharepoint]
requirements: ["EliteaAI/elitea_issues#7262", "EliteaAI/elitea_issues#7345"]
---

# ELITEA-4361: A Microsoft login made while the credential has unsaved edits is not saved

**Module:** toolkits-credentials · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify that a login is not saved if it was made with unsaved changes to the credential form. The sign-in used the typed values, for example a different client ID, so the token may belong to a different app than the saved credential.

---

## Preconditions

- A team project **P**. The tester is a **project admin**.
- A saved Teams credential **C** with app **APP1**'s client ID and no saved login.
- A second Entra app **APP2** with its own client ID and secret.

**Variants:** run for **Teams** and again for a **SharePoint (Delegated)** credential (#7345). For SharePoint, also try an unsaved change of the **site URL** only.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open C. Change **Client ID** and **Client secret** to APP2's values. Do **not** click Save. | The form shows unsaved changes. |
| 2 | Click **Test connection** and complete the Microsoft sign-in. | The toast **"Save the credential first, then log in again: the login must match the saved settings."** appears. |
| 3 | Check the credential GET response in DevTools. | `data.refresh_token` is not set. The saved client ID is still APP1's. |
| 3a | Look at the page's login button right after step 2, then reload. | The page must not show **Logout** as if a login were saved. **Record**: the code keeps the browser token from this sign-in, so the page may show Logout until reload. That would repeat the #7262 confusion. |
| 3b | Without reloading, run a schedule that uses C. | The run asks for a login (nothing stored), whatever the page shows. |
| 4 | Discard the changes and reload C. Click **Test connection** and sign in. | Toast **"Connected! The login is saved for scheduled runs."** The login is now saved for APP1. |

---

## Expected Final State

C has APP1's settings and a login saved for APP1. No login made for APP2 is stored.

---

## Pass/Fail Criteria

**Pass:**
- Step 2 shows the "save the credential first" message and nothing is saved.

**Fail:**
- A login made with unsaved edits is saved on the credential.
- After step 2 the page shows **Logout** as a saved login although nothing is saved (report as a bug).
