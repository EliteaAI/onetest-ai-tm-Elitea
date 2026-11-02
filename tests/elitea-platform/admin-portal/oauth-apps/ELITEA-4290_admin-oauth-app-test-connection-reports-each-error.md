---
id: ELITEA-4290
title: "Admin Portal OAuth app: Test connection reports valid, wrong and blocked credentials"
priority: high
type: functional
module: admin-portal/oauth-apps
status: ready
execution_type: manual
tags: [feat:admin-platform, int:oauth, nfr:security, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4290: Admin Portal OAuth app: Test connection reports valid, wrong and blocked credentials

**Module:** admin-portal/oauth-apps · **Priority:** High · **Type:** Functional

**Objective:** Verify that Test connection checks the client ID, secret and tenant with Microsoft using the unsaved form values, shows a clear message for each failure, and never sends the secret to a host other than `login.microsoftonline.com`.

---

## Preconditions

- Admin user. App `OA_Test_4289` exists with a valid secret.
- Optional: an expired secret, and a tenant that blocks app-only tokens.

---

## Test Data

| Case | Value |
|------|-------|
| Wrong secret | Any random string, or the **Secret ID** instead of the Value |
| Unknown client ID | `00000000-0000-0000-0000-000000000001` |
| Unknown tenant | `https://login.microsoftonline.com/11111111-2222-3333-4444-555555555555` |
| Malformed tenant | `https://login.microsoftonline.com/not-a-tenant!!` |
| Foreign host | `https://example.com/tenant` |
| Plain http | `http://login.microsoftonline.com/organizations` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the app, don't change anything, click **Test connection**. | Button shows "Testing...", then a green alert "The client ID and secret are valid". |
| 2 | Click Replace, enter the wrong secret, Test connection (don't save). | Red alert "The client secret is wrong. Paste the secret Value, not its Secret ID." |
| 3 | (If available) Enter the expired secret, Test. | "The client secret has expired. Create a new one and replace it here." |
| 4 | Enter the valid secret, change Client ID to the unknown one, Test. | "No app with this client ID exists in the tenant of the discovery endpoint." |
| 5 | Restore Client ID, set the unknown tenant endpoint, Test. | "The tenant in the OAuth discovery endpoint does not exist." |
| 6 | Set the malformed tenant, Test. | "The tenant in the OAuth discovery endpoint is not valid." (or a Microsoft error line, no crash). |
| 7 | (If available) Tenant that blocks app-only tokens, Test. | **Yellow warning**: Microsoft accepted the request but would not issue an app-only token. Not an error. |
| 8 | Set the foreign host, Test. | Rejected with "OAuth discovery endpoint must be https://login.microsoftonline.com/<tenant_id or organizations>". No request to example.com (check a request catcher URL if you use one instead). |
| 9 | Set the plain http endpoint, Test. | Same rejection: only https is accepted. |
| 10 | Cancel the dialog and reopen. | The saved values are unchanged: Test connection succeeds again. |
| 11 | Create a new app dialog with all fields valid and Test before saving. | Success. Nothing is created in the list. |

---

## Postconditions

- No changes saved.
