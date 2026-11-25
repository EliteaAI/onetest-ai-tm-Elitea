---
id: ELITEA-4876
title: "Verify correcting configuration and restarting recovers from an error state"
priority: high
type: functional
module: local-mcp
status: draft
execution_type: manual
tags: [r-2.0.9, feat:mcp-local, nfr:usability, nfr:validation]
requirements: [EliteaAI/elitea_issues#7070]
---

## Preconditions

- ELITEA MCP Client build containing #7070 is installed and the tray is running
- A valid token, URL and project ID are available to use as the fix
- `config.json` currently has an invalid token

## Test Data

| Failure | Wrong value | Fix |
|---------|-------------|-----|
| Token | `invalid-token-123` | Valid token |
| URL | `https://does-not-exist.invalid` | Valid deployment URL |
| Project ID | `999999` | Valid project ID |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select **Start MCP Server** with the invalid token | An authentication error is shown |
| 2 | Open Configuration > Settings..., enter a valid token and save | Settings are saved |
| 3 | Select **Start MCP Server** again, without restarting the tray application | The client connects |
| 4 | Check the status, tooltip, notification and the MCP status in `{{base_url}}/app/` | Status is "Connected" and the platform shows the local MCP |
| 5 | Repeat with the invalid token edited back and the fix applied by editing `config.json` directly | The tray detects the change and offers a restart; after it, the client connects |
| 6 | Repeat steps 1-5 for a wrong URL and a wrong project ID | Each recovers the same way |

## Expected Final State

After correcting the value and restarting the connection, the client connects without restarting the tray application.

## Pass/Fail Criteria

**Pass:**
- The error clears and the client connects after each fix
- Both Settings and direct `config.json` edits work
- No tray application restart is required

**Fail:**
- The old error persists after the fix
- A tray application restart is required
- The tray does not detect a direct `config.json` change
