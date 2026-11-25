---
id: ELITEA-4871
title: "Verify SSL certificate failure message and ssl_verify false behavior"
priority: high
type: functional
module: local-mcp
status: draft
execution_type: manual
tags: [r-2.0.9, feat:mcp-local, nfr:usability, nfr:validation]
requirements: [EliteaAI/elitea_issues#7070]
---

## Preconditions

- ELITEA MCP Client build containing #7070 is installed; `elitea-mcp tray`, `serve`, `run` and `doctor` are available
- A deployment URL with an untrusted or self-signed certificate (or a corporate proxy intercepting TLS)
- A valid token and project ID for that deployment

## Test Data

| Field | Value |
|-------|-------|
| `deployment_url` | URL with an untrusted or self-signed certificate |
| `ssl_verify` (first run) | Default (not set) |
| `ssl_verify` (second run) | `false` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Keep `ssl_verify` at the default and select **Start MCP Server** in the tray | An SSL certificate error is shown in the notification and the log; status is not "Connected" |
| 2 | Run `elitea-mcp serve` and `elitea-mcp run` | Both show the SSL error and stop |
| 3 | Set `"ssl_verify": false` in `config.json`, restart the client and start again | The client connects |
| 4 | Compare the status and log with step 1 | They differ: no SSL error, status is "Connected" |
| 5 | Open Help > Run Diagnostics (or run `elitea-mcp doctor`) with `ssl_verify` true | The URL/SSL result lines show the certificate problem, consistent with the tray message |
| 6 | Run Diagnostics again with `ssl_verify` false | The URL/SSL result lines no longer report the certificate failure |

## Expected Final State

With certificate verification on, the client reports a clear SSL error. With `ssl_verify: false`, it connects.

## Pass/Fail Criteria

**Pass:**
- A specific SSL error appears with the default setting in the tray, `serve` and `run`
- `ssl_verify: false` allows the connection
- Diagnostics/`doctor` agree with the tray message

**Fail:**
- The SSL error is generic or missing
- `ssl_verify: false` has no effect
- Diagnostics disagree with the tray
