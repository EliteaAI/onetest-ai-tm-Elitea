---
id: ELITEA-0123
title: "Toolkit and MCP Chipsets Show Exact User-Defined Name"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [nfr:usability, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3535]
---
# ELITEA-0123: Toolkit and MCP Chipsets Show Exact User-Defined Name

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify Toolkit and MCP chipsets display the exact user-configured name (preserving casing and special characters) followed by the tool name.

**Coverage:**
- Toolkit chipset shows exact user-defined name with original casing (e.g., "myJiraTracker: createIssue" not "Myjiratracker" or "my_jira_tracker")
- MCP chipset shows exact user-defined name including special characters like hyphens (e.g., "Slack-MCP: sendMessage")
- No generic or system-generated names used in place of user-defined names
- Name casing and special characters are never normalized or stripped

## Preconditions

- Logged in to ELITEA at {{base_url}}
- A Toolkit configured with user-defined name "myJiraTracker" (mixed casing), exposing tool createIssue
- An MCP configured with user-defined name "Slack-MCP" (hyphen in name), exposing tool sendMessage
- An Agent uses both the Toolkit and MCP
- Browser: Chrome/Edge latest

## Test Data

- Toolkit user-defined name: "myJiraTracker" (mixed casing), tool: createIssue
- MCP user-defined name: "Slack-MCP" (hyphen), tool: sendMessage
- Test prompt: "Create a Jira issue for the new task and send a Slack message about it"
- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA at https://next.elitea.ai/app/. Navigate to Agents in the left sidebar and open the target agent. | Agent detail page loads. |
| 2 | Open the agent's Settings / Toolkits section. Locate the Toolkit entry and read its configured name character by character. | Toolkit is listed with the exact name 'myJiraTracker' (note mixed casing). |
| 3 | Locate the MCP entry in the same section. Read its configured name. | MCP is listed with the exact name 'Slack-MCP' (note hyphen). |
| 4 | Switch to the agent's Chat or Run tab. Enter a prompt that triggers both a Jira toolkit action and a Slack MCP action (e.g., 'Create a Jira issue for the new task and send a Slack message about it'). Press Send. | Agent processes the prompt and invokes both Toolkit and MCP tools. |
| 5 | Wait for the execution to complete. Open the thinking steps / execution trace panel. | Execution trace is visible with chipsets for the Toolkit and MCP tool calls. |
| 6 | Locate the chipset for the Toolkit call (createIssue). Read the full label — note every character including casing. | Chipset label reads exactly 'myJiraTracker: createIssue' — m is lowercase, J and T are uppercase, matching the user-configured name. |
| 7 | Verify the Toolkit chipset does NOT use any altered form of the name (e.g., not Myjiratracker, my_jira_tracker, or Jira Toolkit). | No character substitution, case normalization, or generic replacement is present. |
| 8 | Locate the chipset for the MCP call (sendMessage). Read the full label. | Chipset label reads exactly 'Slack-MCP: sendMessage' — the hyphen between Slack and MCP is preserved. |
| 9 | Verify the MCP chipset does NOT use a generic system name (e.g., not 'MCP Connection 1' or 'SlackMCP'). | MCP chipset label matches the user-configured name exactly. |

## Expected Final State

MCP chipset label matches the user-configured name exactly.

## Pass/Fail Criteria

**Pass:**
- Toolkit chipset label reads exactly "myJiraTracker: createIssue" — original casing preserved
- MCP chipset label reads exactly "Slack-MCP: sendMessage" — hyphen preserved
- No generic replacement names (e.g., "Jira Toolkit", "MCP Connection 1") appear

**Fail:**
- Toolkit name is altered (case-normalized, underscored, or genericized)
- MCP name loses the hyphen or is replaced with a system name
- User-defined name is truncated or substituted
