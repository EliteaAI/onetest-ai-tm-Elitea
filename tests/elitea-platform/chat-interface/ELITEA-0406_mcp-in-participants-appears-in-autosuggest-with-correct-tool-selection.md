---
id: ELITEA-0406
title: "MCP in Participants Appears in `/` Autosuggest With Correct Tool Selection and Mention Format"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [user_story:2925, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#2925]
---
# ELITEA-0406: MCP in Participants Appears in `/` Autosuggest With Correct Tool Selection and Mention Format

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that MCPs added to Participants appear in the `/` autosuggest and follow the same behavior as Toolkits: second dropdown of tools, formatted mention, bold blue highlight.

**Coverage:**
- MCP appears in / dropdown when added to Participants
- MCP tool selection via second dropdown
- /MCPName/toolName format inserted with highlight

## Preconditions

- At least one MCP (e.g., Playwright Browser Automation) configured and added to Participants

## Test Data

- MCP: Playwright Browser Automation
- Tool: navigate (or any available tool)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open chat with MCP in Participants. Type /. | MCP appears in autosuggest dropdown. |
| 2 | Select the MCP from the dropdown. | Second dropdown shows MCP tools. |
| 3 | Select navigate (or any available tool). | Mention /PlaywrightBrowserAutomation/navigate (or equivalent format) inserted in bold blue. |
| 4 | Verify mention format and styling. | Bold + blue, correct /MCPName/toolName path. |

## Expected Final State

Bold + blue, correct /MCPName/toolName path.

## Pass/Fail Criteria

**Pass:**
- MCP appears in autosuggest
- Tool second dropdown works for MCP
- Mention formatted and highlighted correctly

**Fail:**
- MCPs excluded from / dropdown
- Second dropdown missing or empty for MCP
