---
id: ELITEA-4865
title: "Verify non-existent, inaccessible, missing or non-numeric project ID is rejected"
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
- `config.json` has a valid deployment URL and a valid token
- A valid project ID for a project the token's user is not a member of
- Access to the tray log and the console output

## Test Data

| Variant | Setup |
|---------|-------|
| Non-existent project | `project_id: 999999` |
| Project the token's user is not a member of | A valid project ID for another project |
| Missing `project_id` | Key removed from `config.json` |
| Non-numeric `project_id` | `"abc"` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Apply the first variant to `config.json` | Configuration is saved |
| 2 | In the tray, select **Start MCP Server** | A specific project message is shown (no access to the project, or the project does not exist; check `project_id` in config); status is never "Connected" |
| 3 | Check the tray notification, tooltip and log | Same message in all places |
| 4 | Repeat steps 1-3 for the other variants | Each variant shows its own project-related message; the missing key reports that the project ID is not set |
| 5 | Run `elitea-mcp serve` for each variant | Console shows the project message and the process stops |
| 6 | Run `elitea-mcp run` for each variant | Console shows the project message and the process stops |
| 7 | Open `{{base_url}}/app/` > MCPs | No server registered by this client appears |

## Expected Final State

The client does not connect for any invalid project configuration. Messages point to `project_id`, and nothing from this client is registered in ELITEA.

## Pass/Fail Criteria

**Pass:**
- 403 and 404 cases show a clear project access or project-not-found message
- Missing and non-numeric `project_id` are reported before any connection
- Behavior is the same in the tray, `serve` and `run`
- No server is registered in ELITEA

**Fail:**
- Any variant shows "Connected"
- The message is generic or unrelated to the project
- The client crashes or hangs on a non-numeric value
