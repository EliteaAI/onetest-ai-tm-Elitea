---
id: ELITEA-4866
title: "Verify wrong deployment URL ends with a final specific error and no endless retry"
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
- `config.json` has a valid token and `project_id`
- Access to the tray log and the console output

## Test Data

| Variant | URL |
|---------|-----|
| Unresolvable host | `https://does-not-exist.invalid` |
| Refused connection | `http://localhost:9` |
| Timeout | A blackholed address or a firewall-blocked host |
| Non-ELITEA site returning HTML | `https://example.com` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set `deployment_url` to the first variant | Configuration is saved |
| 2 | In the tray, select **Start MCP Server** | A "Connecting..." state is shown, then a final specific error |
| 3 | Watch the tray for at least 2 minutes and count connection attempts in the log | Attempts are limited; the tray is not stuck on "Starting socket connection..." |
| 4 | Read the final status | The error names the cause: DNS lookup failed, connection refused, timed out (check URL, VPN or proxy), or "responded but is not an ELITEA API (received HTML)" |
| 5 | Repeat steps 1-4 for the other variants | Each variant ends with its own final error |
| 6 | Run `elitea-mcp serve` for each variant | Console shows the final error and the process stops |
| 7 | Run `elitea-mcp run` for each variant | Console shows the final error and the process stops |

## Expected Final State

For every wrong URL the client stops after a limited number of attempts with a specific final error. The tray is not left in a connecting state.

## Pass/Fail Criteria

**Pass:**
- Each variant ends with a final specific error in the tray, console and log
- The number of attempts is limited
- `serve` and `run` exit

**Fail:**
- The tray stays on "Starting socket connection..." or retries silently without end
- The message does not name the cause
- The process does not stop in `serve` or `run`
