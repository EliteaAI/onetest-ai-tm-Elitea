---
id: ELITEA-4356
title: "[Parametrized] A Microsoft login on the credential page is saved on the credential and used by a scheduled run"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, issue:7262, issue:7037, stored-login, p0]
requirements: ["EliteaAI/elitea_issues#7262", "EliteaAI/elitea_issues#7037"]
---

# ELITEA-4356: [Parametrized] A Microsoft login on the credential page is saved on the credential and used by a scheduled run

**Module:** toolkits-credentials · **Priority:** Critical (P0) · **Type:** Functional

**Objective:** Verify that signing in to Microsoft from the **credential page** (Test connection / Login) saves the login on the credential, the same way the toolkit page's Login bar does. A scheduled pipeline, which runs without any browser, must then be able to use it. Before #7262, this login stayed in the browser only, although the page showed **Logout**.

---

## Preconditions

- A Microsoft Entra app registration with a client ID, a client secret and delegated permissions for the scopes used below, including `offline_access`.
- A Microsoft test account **MS-A** that can consent to those permissions.
- A team project **P**. The tester is a **project admin** in P.
- Browser **A**, with no earlier sign-in to MS-A in the ELITEA tab.

---

## Test Data

| Variant | Credential type | Scopes / settings | Tool used by the pipeline |
|---|---|---|---|
| Teams | Teams | `ChannelMessage.Read.All`, `User.Read` | List joined teams |
| Outlook | Outlook | `Mail.Read`, `User.Read` | Read recent emails |
| Dataverse | Dataverse | Tenant ID and the `*.dynamics.com` URL of a test environment | List tables |

Run the steps once per variant.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In P, create a credential of the variant's type with the app's client ID, client secret, discovery endpoint `https://login.microsoftonline.com/<tenant_id>` (Teams / Outlook) and scopes from **Test Data**. Click **Save**. | The credential is saved. The page shows **Test connection** and no **Logout**. |
| 2 | Click **Test connection** and complete the Microsoft sign-in as MS-A. | The sign-in window closes. The toast **"Connected! The login is saved for scheduled runs."** appears. The page shows **Logout**. |
| 3 | Open DevTools → Network. Reload the credential page and check the `GET /api/v2/configurations/configuration/<project>/<id>` response. | `data.refresh_token` is present and is a `{{secret.<id>}}` reference, not a raw token. |
| 4 | In P, create a toolkit of the variant's type that uses this credential, and a pipeline with one node that calls the tool from **Test Data**. Save the pipeline. | The pipeline is saved. |
| 5 | Add a schedule to the pipeline that runs in 2–3 minutes. Close browser A completely. | — |
| 6 | After the scheduled time, open the pipeline's run history in any browser. | The scheduled run is **finished**, and the tool output shows real data from MS-A (team names, email subjects or Dataverse tables). It does not show a "log in" prompt or an authorization error. |

---

## Expected Final State

The login made on the credential page is saved on the credential, and scheduled runs use it without any browser.

---

## Pass/Fail Criteria

**Pass:**
- The toast in step 2 says the login is saved for scheduled runs.
- `data.refresh_token` is a `{{secret.…}}` reference in step 3.
- The scheduled run in step 6 returns MS-A's data.

**Fail:**
- The page shows **Logout** but `data.refresh_token` is missing, which is the #7262 bug.
- The scheduled run asks for a login or fails with an authorization error.
- The raw refresh token is visible in the GET response.
