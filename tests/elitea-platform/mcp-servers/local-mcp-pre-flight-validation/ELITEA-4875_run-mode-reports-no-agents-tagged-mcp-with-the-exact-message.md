---
id: ELITEA-4875
title: "Verify run mode reports no agents tagged mcp with the exact message"
priority: high
type: functional
module: local-mcp
status: draft
execution_type: manual
tags: [r-2.0.9, feat:mcp-local, nfr:usability, nfr:validation]
requirements: [EliteaAI/elitea_issues#7070]
---

## Preconditions

- ELITEA MCP Client build containing #7070 is installed; `elitea-mcp run` and `serve` are available
- Valid URL, token and project ID (the token has access to the project)
- Project A has no agents tagged `mcp`; at least one agent in project A exists without the `mcp` tag
- Project B has at least one agent tagged `mcp`

## Test Data

| Field | Value |
|-------|-------|
| Expected message | `No agents tagged "mcp" in project <project_id>. Add the "mcp" tag to the agents you want to expose.` |
| Similar tags to try | `MCP`, `mcp-test`, ` mcp` |
| Other errors | Invalid token; non-existent project ID |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set `project_id` to project A in `config.json` and run `elitea-mcp run` | The expected message is printed |
| 2 | Check the message text | It has the tag name `"mcp"` in quotes, the correct project number and the instruction to add the `mcp` tag |
| 3 | Change `project_id` to another valid project without tagged agents and run again | The message shows the new project number |
| 4 | Check the process end state | Non-zero exit code, no hang, no silent retry; no MCP tools are exposed |
| 5 | Compare with other errors | The message is not "Failed to fetch agent details", not a JSON decode error, and not an authentication or project access message |
| 6 | Check the log with Debug Logging off and on | The message appears once; no token or raw response body appears |
| 7 | Tag one agent in project A with `mcp` and run again without changing the configuration | The message no longer appears and the tagged agent is exposed |
| 8 | Tag the agent with each similar tag and run again | Record whether each is treated as tagged |
| 9 | Run `elitea-mcp run` with an invalid token, then with a non-existent project ID | Each shows its own authentication or project message, not the "No agents tagged" message |
| 10 | Run `elitea-mcp serve` against project A | `serve` does not show the "No agents tagged" message |

## Expected Final State

`run` stops with the exact "No agents tagged" message when the tag lookup returns nothing, and exposes agents once they are tagged.

## Pass/Fail Criteria

**Pass:**
- The exact message with the correct project number appears
- The process stops cleanly with a non-zero exit code and exposes no tools
- The message is distinct from authentication, project access and connection errors
- Tagging an agent removes the message and exposes the agent
- `serve` does not show this message

**Fail:**
- The text differs from the expected message or the project number is wrong
- A generic or JSON decode error appears instead
- The process hangs, or the message is repeated or leaks secrets
