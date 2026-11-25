---
id: ELITEA-4869
title: "Verify UI-link deployment URL is normalized to the base URL and connects"
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
- A valid token and a valid `project_id` for `{{base_url}}`
- Access to the tray log and the console output

## Test Data

| Input | Form |
|-------|------|
| `{{base_url}}/app/13/mcp` | UI link with path |
| `{{base_url}}/` | Trailing slash |
| `{{base_url}}/app/` | App root |
| `{{base_url}}/app/13/mcp?x=1#y` | Query string and fragment |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Enter the first input as the deployment URL in Settings... (or `config.json`) with the valid token and project ID | Configuration is saved |
| 2 | Select **Start MCP Server** | A message advises using the base URL, and the client connects |
| 3 | Check the effective URL in the log | It is the base URL, without path, query string or fragment |
| 4 | Open Configuration > View Current Config | The shown URL is consistent with the entered value and the effective URL |
| 5 | Repeat steps 1-4 for the other inputs | Each input is reduced to the base URL and connects |
| 6 | Run `elitea-mcp serve` for each input | The client connects; no unrelated socket or JSON error |
| 7 | Run `elitea-mcp run` for each input | The client connects; no unrelated socket or JSON error |

## Expected Final State

Every URL form is reduced to the base URL and the client connects with the final status "Connected".

## Pass/Fail Criteria

**Pass:**
- A hint about the base URL is shown for UI links
- The effective URL in the log is the base URL for every input
- The client connects in the tray, `serve` and `run`

**Fail:**
- The client fails with an unrelated socket or JSON decode error
- The effective URL still contains the path, query string or fragment
