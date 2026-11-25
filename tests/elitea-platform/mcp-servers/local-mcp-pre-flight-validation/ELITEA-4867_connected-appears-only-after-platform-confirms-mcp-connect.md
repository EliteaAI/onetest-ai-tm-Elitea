---
id: ELITEA-4867
title: "Verify Connected appears only after the platform confirms mcp_connect"
priority: critical
type: functional
module: local-mcp
status: draft
execution_type: manual
tags: [r-2.0.9, feat:mcp-local, nfr:usability, nfr:validation]
requirements: [EliteaAI/elitea_issues#7070]
---

## Preconditions

- ELITEA MCP Client build containing #7070 is installed and the tray is runnable
- A valid deployment URL, token and project ID
- A project the token's user does not belong to
- Access to the tray log

## Test Data

| Case | Setup |
|------|-------|
| Valid | Valid URL, token and a project the user belongs to |
| Not a member | Valid URL and token, `project_id` of a project the user does not belong to |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start the client with the Valid case and observe the tray status text, tooltip and status dot from Start to the final state | Status shows "Connecting..." first, then "Connected" |
| 2 | Check the log for the "Connecting..." and "Connected" messages | Both are present and "Connecting..." comes first |
| 3 | Open `{{base_url}}/app/` > MCPs | The local MCP status matches the client |
| 4 | Stop the client. Start it with the Not a member case | The client does not show "Connected" |
| 5 | Wait at least 60 seconds and observe the tray status and the log | The status never becomes "Connected"; a specific message or a clear waiting state is shown |
| 6 | Open `{{base_url}}/app/` > MCPs and compare with the client status | Client and platform views agree |

## Expected Final State

"Connected" is shown only after the platform confirms the connection. When the platform does not confirm, the client never shows "Connected".

## Pass/Fail Criteria

**Pass:**
- "Connecting..." precedes "Connected" in the tray and the log
- Without platform confirmation the status is never "Connected" after 60 seconds
- Client and platform statuses agree

**Fail:**
- "Connected" appears when only the socket is open
- The tray status and the platform view disagree
