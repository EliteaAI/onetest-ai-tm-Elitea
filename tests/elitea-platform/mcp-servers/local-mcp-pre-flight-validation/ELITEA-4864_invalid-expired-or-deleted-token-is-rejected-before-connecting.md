---
id: ELITEA-4864
title: "Verify invalid, expired or deleted token is rejected before connecting"
priority: critical
type: functional
module: local-mcp
status: draft
execution_type: manual
tags: [r-2.0.9, feat:mcp-local, nfr:usability, nfr:validation]
requirements: [EliteaAI/elitea_issues#7070]
---

## Preconditions

- ELITEA MCP Client build containing #7070 is installed; `elitea-mcp tray`, `serve` and `run` are available
- `config.json` has a valid deployment URL and a valid numeric `project_id` the token can access
- At least one local STDIO MCP server is configured in `config.json`
- Access to the tray log, `%TEMP%\elitea-mcp\` and the console output

## Test Data

| Variant | Token value |
|---------|-------------|
| Random string | `invalid-token-123` |
| Expired token | Personal token created with a short expiration, used after it expired |
| Deleted token | Personal token deleted in `{{base_url}}` Settings > Personal Tokens |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set `auth_token` in `config.json` (or via Settings...) to the first variant | Configuration is saved |
| 2 | In the tray, select **Start MCP Server** | A specific authentication error is shown (token invalid or expired, generate a new one in Settings > Tokens); status is never "Connected" |
| 3 | Check the tray notification, tooltip, first menu line and tray log | All show the same authentication error; no raw response text |
| 4 | Repeat steps 1-3 for the other two variants | Each variant shows the authentication error |
| 5 | Run `elitea-mcp serve` for each variant | Console shows the authentication error and the process stops |
| 6 | Run `elitea-mcp run` for each variant | Console shows the authentication error and the process stops |
| 7 | Open `{{base_url}}/app/` > MCPs and check the local MCP status | No server from this client is shown as connected |

## Expected Final State

The client does not connect with any invalid token. The error message identifies the token as the problem in the tray, console and log, and ELITEA shows no connected local MCP.

## Pass/Fail Criteria

**Pass:**
- Every variant shows a specific authentication message in the tray and the console/log
- Status is never "Connected" for any variant in the tray, `serve` or `run`
- ELITEA shows no connected local MCP from this client

**Fail:**
- Any variant shows "Connected"
- The message is generic, a JSON decode error or a socket error instead of an authentication message
- The process hangs or retries silently
