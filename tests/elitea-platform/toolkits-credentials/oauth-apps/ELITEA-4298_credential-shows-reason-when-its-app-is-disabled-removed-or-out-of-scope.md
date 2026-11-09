---
id: ELITEA-4298
title: "Credential shows a clear reason when its app is disabled, switched off, out of scope or deleted"
priority: high
type: negative
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4298: Credential shows a clear reason when its app is disabled, switched off, out of scope or deleted

**Module:** toolkits-credentials/oauth-apps · **Priority:** High · **Type:** Negative

**Objective:** Verify that a credential on an admin app that no longer applies shows why and offers "Switch to Custom app", that agent runs and sign-in fail with the same reason, and that restoring the app restores the credential without user action.

---

## Preconditions

- Apps **X** and **Y** for team project pr_E, both **not** Default (so the user picked X).
- U1 in pr_E has **C_T** (Teams) and **C_O** (Outlook), both saved on X, signed in, used by toolkits in agent **AG_4298**.

---

## Test Data

| Admin change | Expected message on the credential |
|--------------|------------------------------------|
| X disabled | "X was disabled by your administrator. Switch to Custom app." |
| Teams off on X | "X is no longer offered for Teams credentials by your administrator. Switch to Custom app." |
| pr_E removed from X | "The Microsoft Entra ID app selected for this credential is not available in this project. Switch to Custom app." |
| X deleted | "The Microsoft Entra ID app selected for this credential no longer exists. Switch to Custom app." |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Admin, **disable** X. As U1 open C_T. | App picker in error state: "X was disabled by your administrator. Switch to Custom app." |
| 2 | Run AG_4298 with a Teams prompt. | Fails with the same reason, no crash, no secret in the error. |
| 3 | Re-enable X. Reopen C_T and run AG_4298. | No error. Run works **without** a new sign-in or any user edit. |
| 4 | Switch **Teams off** on X. Open C_T and C_O. | C_T: "X is no longer offered for Teams credentials…". C_O: no error, still works. |
| 5 | Switch Teams on. Change X's Projects to another project only (remove pr_E). Open C_T. | "…not available in this project. Switch to Custom app." The app name is **not** shown. |
| 6 | Restore pr_E on X. | C_T works again. |
| 7 | Call the sign-in proxy for C_T while X is disabled (repeat step 1 state). | 400, `error: "app_unavailable"`, a readable `error_description`. |
| 8 | Delete X. Open C_T. | "The Microsoft Entra ID app selected for this credential no longer exists. Switch to Custom app." (UI fallback if the server sends no reason: "This app is no longer available. Switch to Custom app."). Record which text is shown. |
| 9 | Pick **Y** in the picker and Save. | Saved. After one sign-in, the run works. |
| 10 | On C_O (still X-deleted), switch to **Custom app**, enter own client, Save. | Saved. Works with own app after sign-in. |

---

## Postconditions

- Delete Y and test credentials.
