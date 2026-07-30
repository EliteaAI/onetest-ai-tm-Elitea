---
id: ELITEA-2221
title: "[EliteaAI/elitea_issues#5294] Login Button Triggers Correct Auth Flow — OAuth 2.0 and Custom Headers"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-2221: [EliteaAI/elitea_issues#5294] Login Button Triggers Correct Auth Flow

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking the login button initiates the correct authentication flow for OAuth 2.0 and Custom Headers auth types.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Test MCPs configured: one with OAuth 2.0 Client Credentials auth, one with Custom Headers auth
- Both MCPs added to separate Chat conversations or Agent toolkits
- Both MCPs currently in unauthenticated state (login button visible, logout button hidden)

## Test Data

| Auth Type | MCP Config | Credentials |
|-----------|-----------|-------------|
| OAuth 2.0 | client_id, client_secret, token_url | Valid test credentials |
| Custom Headers | header names and values | Valid test header values |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Chat with unauthenticated OAuth 2.0 MCP, click Login button. | Login flow initiated. Browser may redirect to auth provider or show modal. |
| 2 | (OAuth 2.0 only) Complete OAuth 2.0 flow: approve scopes, confirm login. | OAuth provider redirects back to ELITEA with authorization code. |
| 3 | Observe API calls: verify POST to /api/mcp/authorize with client_id, client_secret. | Request made to correct OAuth 2.0 token endpoint with correct credentials. |
| 4 | Verify response contains access_token (and optional refresh_token). | Backend successfully exchanges code/credentials for access token. |
| 5 | Confirm UI updates: login button hidden, logout button visible, status shows "Authenticated". | MCP now shows authenticated state. |
| 6 | In separate Chat with unauthenticated Custom Headers MCP, click Login button. | Login flow initiated for Custom Headers MCP. |
| 7 | Verify system validates and applies custom headers (headers stored and used in MCP requests). | Custom headers are accepted and stored. |
| 8 | Confirm UI updates: login button hidden, logout button visible for Custom Headers MCP. | Custom Headers MCP now shows authenticated state. |

## Expected Final State

- OAuth 2.0 MCP successfully authenticated with access token
- Custom Headers MCP successfully authenticated with headers applied
- Both MCPs show logout button and "Authenticated" status
- Both can invoke tools without auth errors

## Pass/Fail Criteria

**Pass:** OAuth 2.0 and Custom Headers flows complete; tokens/headers applied; UI reflects authenticated state; tools can be invoked.  
**Fail:** Login fails for either auth type; tokens/headers not stored; UI does not update; tools cannot be invoked post-login.
