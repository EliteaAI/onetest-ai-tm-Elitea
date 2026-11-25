---
id: ELITEA-4868
title: "Verify pre-flight failure happens before any socket connection"
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
- Access to the tray log and the console output

## Test Data

| Field | Value |
|-------|-------|
| Single failing value | `auth_token`: `invalid-token-123` |
| Two failing values | `deployment_url`: `https://does-not-exist.invalid` and `auth_token`: `invalid-token-123` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set the single failing value in `config.json` | Configuration is saved |
| 2 | In the tray, open Logs and select **Enable Debug Logging** | Debug logging is enabled |
| 3 | Select **Start MCP Server** and check the log | No socket connect attempt and no "Connected to platform" text appears; the pre-flight error is shown |
| 4 | Run `elitea-mcp serve` and check the console | No socket connect attempt and no "Connected to platform" message |
| 5 | Run `elitea-mcp run` and check the console | No socket connect attempt and no "Connected to platform" message |
| 6 | Set the two failing values and start from the tray | Exactly one failing check is reported |
| 7 | Note which check is reported, and repeat with `serve` and `run` | The same check is reported in every entry point |

## Expected Final State

When any pre-flight check fails, the client stops before opening a socket and reports a single failing check.

## Pass/Fail Criteria

**Pass:**
- No socket connection or "Connected to platform" text appears after a pre-flight failure in the tray, `serve` and `run`
- Only one failing check is reported when two values are wrong
- The reported check is the same across entry points

**Fail:**
- A socket connect attempt or "Connected to platform" appears despite a failed check
- Several failures are reported together, or the reported check differs between entry points
