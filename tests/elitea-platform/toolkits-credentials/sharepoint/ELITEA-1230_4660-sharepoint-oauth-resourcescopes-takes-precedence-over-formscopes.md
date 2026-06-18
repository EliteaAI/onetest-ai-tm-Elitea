---
id: ELITEA-1230
title: "[EliteaAI/elitea_issues#4660] SharePoint OAuth — `resourceScopes` Takes Precedence Over `formScopes` in Auth Modal"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:credentials, int:sharepoint, feat:toolkits, issue:4660, int:oauth, r-2.0.3]
requirements: [4660]
---
# ELITEA-1230: [EliteaAI/elitea_issues#4660] SharePoint OAuth — `resourceScopes` Takes Precedence Over `formScopes` in Auth Modal

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the scope precedence fix in `McpAuthModal.jsx`: `resourceScopes` (backend-computed, always includes `offline_access`) must take priority over user-configured `formScopes` when building the OAuth authorization URL. This prevents user-configured scopes from silently discarding `offline_access` — the root cause of the original bug.

## Preconditions

SharePoint toolkit configured with a custom OAuth scope in the toolkit configuration form (e.g., `https://graph.microsoft.com/.default`)
Browser DevTools Network tab open to inspect popup URL
User is not currently authenticated

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the SharePoint toolkit credential configuration and set a custom OAuth scope (e.g., `https://graph.microsoft.com/.default`). Save the configuration. | Custom scope saved in the toolkit form. |
| 2 | Click 'Logon'. Capture the Microsoft OAuth authorization popup URL (visible in popup address bar or intercepted in Network tab). | Authorization URL is opened with the Azure AD endpoint. |
| 3 | Examine the `scope` query parameter in the authorization URL. | `offline_access` is present in the scope, alongside or before the custom `formScope` value. Example: `scope=offline_access+https%3A%2F%2Fgraph.microsoft.com%2F.default`. The `resourceScopes` from the backend (which includes `offline_access`) took precedence. |
| 4 | Complete the authentication. Check sessionStorage for `refresh_token`. | Azure AD returned a `refresh_token` because `offline_access` was successfully included in the request. Token stored in sessionStorage with both `access_token` and `refresh_token`. |

## Expected Final State

Azure AD returned a `refresh_token` because `offline_access` was successfully included in the request. Token stored in sessionStorage with both `access_token` and `refresh_token`.

## Pass/Fail Criteria

`offline_access` present in authorization URL scope even when custom `formScopes` are configured
`resourceScopes` used when non-empty; `formScopes` only used as fallback when `resourceScopes` is empty
Refresh token returned by Azure AD after the authentication (confirms `offline_access` was in the request)
