---
id: ELITEA-4300
title: "OAuth sign-in proxy and credential API enforce the app rules and never expose the app secret"
priority: critical
type: security
module: toolkits-credentials/oauth-apps
status: ready
execution_type: manual
tags: [feat:credentials, nfr:security, int:oauth, issue:7149, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7149"]
---

# ELITEA-4300: OAuth sign-in proxy and credential API enforce the app rules and never expose the app secret

**Module:** toolkits-credentials/oauth-apps · **Priority:** Critical · **Type:** Security

**Objective:** Verify on the API level that the server, not the UI, enforces the rules: the proxy uses only the app's own token endpoint and the admin's scopes, checks the credential type and project, works with MCP exposure off, and that credential writes that bypass the form are rejected. No response may contain the secret.

---

## Preconditions

- App **A** (Teams + Outlook on, SharePoint **off**) for team project pr_F, not Default. App **B** for project pr_G only.
- U1 is editor in pr_F. Keycloak JWT. A valid authorization `code` captured from a Teams sign-in on A (DevTools; codes are single-use, capture a new one per step).
- A request-catcher URL you control, for the forged endpoint.
- Admin can switch MCP exposure off (step 7).

---

## Test Data

| Item | Value |
|------|-------|
| Proxy | `POST /api/v2/elitea_core/mcp_oauth_proxy/{pr_F}` |
| Forged endpoint | `https://<request-catcher>/token` |
| Forged scope | `Mail.ReadWrite Files.ReadWrite.All` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Replay a Teams sign-in to the proxy with `oauth_app_id: A`, `credential_type: "teams"` and `token_endpoint` = forged endpoint. | Exchange succeeds against Microsoft. The request catcher receives **nothing**. |
| 2 | Same with `scope` = forged scope. | The token's `scp` (decode the access token) contains only A's Teams scopes (+ offline_access), not Mail.ReadWrite / Files.ReadWrite.All. |
| 3 | Same without `credential_type`. | 400 `app_unavailable`. |
| 4 | Same with `credential_type: "sharepoint"` (off on A). | 400 `app_unavailable`. |
| 5 | Same with `credential_type: "jira"`. | 400, "Unsupported credential type: jira". |
| 6 | Same with `oauth_app_id: B` (not assigned to pr_F). | 400 `app_unavailable`. |
| 7 | Admin switches MCP exposure off. Repeat step 1 with a fresh code. Then call the proxy **without** `oauth_app_id` (plain MCP exchange). | App sign-in: 200. Plain MCP exchange: 403 "MCP exposure is disabled on this deployment". Restore MCP exposure. |
| 8 | Check the responses of steps 1 – 7, the user `oauth_apps` list, credential GET/list and test connection. | No `client_secret` value anywhere. |
| 9 | POST a Teams credential in pr_F with `oauth_app_id: B`. | Rejected: app not available in this project. |
| 10 | Disable A. PUT a credential with `oauth_app_id: A`. | Rejected with the disabled reason. Re-enable A. |
| 11 | POST a Teams credential with `shared: true`. | 400 "Teams credentials cannot be shared". |
| 12 | **Record (S1, not built):** make A Default, then POST a Custom Teams credential (own client_id/secret, no oauth_app_id) in pr_F. | Spec: rejected ("Custom app where a Default applies"). Record actual. |
| 13 | **Record (S1, not built):** A and a second app for pr_F, none Default. POST a Teams credential with neither `oauth_app_id` nor own client. | Spec: rejected (missing pick). Record actual. |
| 14 | Check agent run logs (if accessible) after a Default app run. | No secret value in logs. |

---

## Postconditions

- Restore A (enabled, not Default), MCP exposure, delete test credentials.
