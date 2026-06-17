---
id: ELITEA-0726
title: "[#5116] MCP Configuration (MCPs Page): Secret Field Shows \"New Secret\" Shortcut"
priority: critical
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [feat:credentials, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5116]
---
# ELITEA-0726: [#5116] MCP Configuration (MCPs Page): Secret Field Shows "New Secret" Shortcut

**Module:** Mcp Servers · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that on the dedicated MCPs configuration page (both create and edit flows), secret fields in Secret mode expose the "New Secret" shortcut button and it functions correctly.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- User has MCP create/edit and secret create/list permissions
- A Remote MCP with an OAuth2 Client Secret field is accessible (e.g., remote_github_mcp) or can be created

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to MCPs in the sidebar. | MCPs list page loads. |
| 2 | Open an existing Remote MCP (e.g., remote_github_mcp) by clicking its card. | MCP configuration page opens with the Configuration section visible. |
| 3 | In the Configuration section, locate the Client Secret field. Ensure it is in Secret mode (not Password mode). | Client Secret field is in Secret mode with a combobox visible. |
| 4 | Open the secret selection dropdown. | Dropdown opens showing: (1) a CREATE section with the correct label for the project type ('New Private Secret' or 'New Project Secret'); (2) a SAVED SECRETS section with a refresh icon. |
| 5 | Click the CREATE option in the dropdown. | Settings → Secrets page opens in a new browser tab with ?createSecret=1 in the URL. The MCP configuration tab remains open and unchanged. |
| 6 | Repeat steps 2–5 using the Create MCP flow: click Create, select Remote type, fill in a name and URL, and open the Client Secret dropdown. | The same CREATE section and refresh icon are present in the secret dropdown on the MCP Create form. |

## Expected Final State

The same CREATE section and refresh icon are present in the secret dropdown on the MCP Create form.

## Pass/Fail Criteria

**Pass:** CREATE section with correct label and refresh icon visible on both the MCP Edit and MCP Create forms; clicking CREATE opens new tab with ?createSecret=1.
**Fail:** CREATE section absent on MCP configuration page; wrong label; no new tab opened; feature works on credentials page but not on MCP page.
