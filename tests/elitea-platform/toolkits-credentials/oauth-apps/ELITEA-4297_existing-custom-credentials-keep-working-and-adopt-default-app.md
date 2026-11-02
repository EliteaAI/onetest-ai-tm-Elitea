---
id: ELITEA-4297
title: "Existing Custom credentials keep working, then adopt a Default app on next use (SharePoint App-only excluded)"
priority: critical
type: functional
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:oauth, int:sharepoint, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4297: Existing Custom credentials keep working, then adopt a Default app on next use (SharePoint App-only excluded)

**Module:** toolkits-credentials/oauth-apps · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that credentials with the user's own app keep working while no Default app applies, and that once a Default app applies they switch to it on next use (option B): the switch is stored, the user signs in once again, own fields stay in the database, and SharePoint App-only is never switched.

---

## Preconditions

- Team project pr_D with **no** apps; Public has no Default (disable the seeded app or turn Default off).
- U1 in pr_D owns, created with their own Entra app and signed in:
  - **C_OL** Outlook Custom (Delegated), used by toolkit **TK_OL** in agent **AG_4297**.
  - **C_SP_DEL** SharePoint Delegated, **C_SP_APP** SharePoint **App-only**.
- Admin app **D** for pr_D, prepared and **disabled**.

---

## Test Data

| Item | Value |
|------|-------|
| Prompt | "Read my latest email" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As U1, open C_OL. | Opens on **Custom app** fields with its own values (or plain Custom form). Leaving gives no unsaved warning. |
| 2 | Run AG_4297 with the prompt. | Works with the own app; no new sign-in needed. |
| 3 | As Admin, enable D (**not** Default). As U1 reopen C_OL. | Switcher shown, **Custom app** preselected with own values. GET credential: no `oauth_app_id`. |
| 4 | Run AG_4297. | Still uses the own app (sign-in prompt / Network client ID = own). Nothing changes in stored data. |
| 5 | As Admin, make D **Default**. As U1, run AG_4297 **without** opening the form. | Run asks U1 to **sign in once** (old sign-in made with the own client is not used). After sign-in, the run works with D's client ID. |
| 6 | GET C_OL via API. | `oauth_app_id` = D's uuid (stored by the handler). |
| 7 | (DB / support access, optional) Check C_OL row. | Own client_id and secret reference are still stored, unused. |
| 8 | Open C_OL in the form. | No switcher, "Sign-in settings are managed by your administrator.", no Custom fields. |
| 9 | Open **C_SP_DEL**. | Switched to D the same way (no switcher). |
| 10 | Open **C_SP_APP** and run a SharePoint App-only tool. | **Not switched**: keeps its own client ID and secret, App-only mode, works. |
| 11 | As Admin, turn **Default off** on D (D stays enabled). Reopen C_OL. | Switcher returns. C_OL **stays on D** (Default app tab), not back on own app. |
| 12 | Switch C_OL to **Custom app**. | The own client ID and endpoint values come back. Save. GET: no `oauth_app_id`. |
| 13 | Run AG_4297. | Asks for sign-in once more (client changed back); then works with the own app. |
| 14 | Make D Default again, then create app **D2** for pr_D and make it Default instead (D Default off). Run AG_4297. | C_OL switches to **D2** on next use with one more sign-in. |
| 15 | **Record:** an existing credential that was **Shared** before the feature. | Spec: stays shared until edited; Shared toggle not offered on edit. |

---

## Postconditions

- Disable D and D2, delete test data.
