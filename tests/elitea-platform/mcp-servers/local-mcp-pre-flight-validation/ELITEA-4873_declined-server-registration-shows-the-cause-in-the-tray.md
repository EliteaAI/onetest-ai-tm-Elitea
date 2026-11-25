---
id: ELITEA-4873
title: "Verify declined server registration shows the cause in the tray"
priority: high
type: functional
module: local-mcp
status: draft
execution_type: manual
tags: [r-2.0.9, feat:mcp-local, nfr:usability, nfr:validation]
requirements: [EliteaAI/elitea_issues#7070]
---

## Preconditions

- ELITEA MCP Client build containing #7070 is installed on two clients (A and B), or one client plus a stale session
- Both use the same deployment, token and project
- Access to client B's tray, log and console

## Test Data

| Field | Value |
|-------|-------|
| Server name | `github` (same on both clients) |
| Project | The same `project_id` on both clients |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start client A with server `github` and wait for "Connected" | Client A is connected |
| 2 | Start client B (another machine, or `elitea-mcp serve` in a second terminal) with the same server name and project | Client B starts |
| 3 | Check client B's tray, log and console | A message says the server `github` was declined, with the reason and the project number |
| 4 | Compare the message with the issue's proposed text | It contains the server name, "was declined", the reason and the project number |
| 5 | Check client B's tray status | It does not read as a fully healthy connection for the declined server |
| 6 | Stop client A and restart client B | Registration of `github` now succeeds |

## Expected Final State

A declined registration is reported with its cause. After the conflict is removed, the server registers.

## Pass/Fail Criteria

**Pass:**
- The declined message appears in the tray, log and console
- It includes the server name, reason and project number
- The status does not look fully healthy while the server is declined
- Registration succeeds after client A stops

**Fail:**
- The decline is silent or the message has no cause
- The tray shows a fully healthy connection for a declined server
- Registration still fails after client A stops
