---
id: ELITEA-2744
title: "Verify agent message displays toolkit name when MCP authorization is needed"
priority: critical
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp-local, feat:mcp-remote, nfr:usability, r-2.0.6]
requirements: [EliteaAI/elitea_issues#5637]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to a project with Admin/Editor permissions
- Agent with attached MCP(s) that require authorization exists

## Test Data

| MCP Type | MCP Name | Description |
|----------|----------|-------------|
| Remote MCP | GitHub Toolkit | Toolkit allows users to connect to Atlassian (or any remote MCP) |
| Local MCP | Epam Stuffing | Local MCP toolkit |
| Preconfigured Remote | Weather API | Preconfigured remote MCP |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/agents/` | Agents list page loads |
| 2 | Open an Agent with an attached **Remote MCP** (e.g., "GitHub Toolkit") that requires authorization | Agent page loads, MCP visible in Tools section with "Log in" button (NOT logged in) |
| 3 | **DO NOT click "Log in"** - go directly to the Right Chat part inside Agent | Right Chat part inside Agent opens |
| 4 | Send a message that requires the MCP to be used (e.g., "Get my GitHub repositories") | Agent responds with a message indicating authorization is needed |
| 5 | Verify the agent message content | Message displays the **toolkit name** "GitHub Toolkit" and its characteristics/description so user understands which specific MCP needs authorization |
| 6 | Repeat steps 2-5 with a **Local MCP** attached | Agent message displays the Local MCP toolkit name (e.g., "Epam Stuffing") and its characteristics |
| 7 | Repeat steps 2-5 with a **Preconfigured Remote MCP** attached | Agent message displays the Preconfigured MCP toolkit name and characteristics |

## Expected Final State

For all MCP types (Remote, Local, Preconfigured Remote), when authorization is needed, the agent's message clearly identifies:
- The specific toolkit name
- Toolkit characteristics/description
- That authorization is required

## Pass/Fail Criteria

**Pass:**
- Agent message for Remote MCP shows toolkit name and characteristics
- Agent message for Local MCP shows toolkit name and characteristics
- Agent message for Preconfigured Remote MCP shows toolkit name and characteristics
- User can clearly understand which specific toolkit needs authorization

**Fail:**
- Agent message doesn't display toolkit name
- Agent shows generic message without identifying the specific MCP
- Toolkit characteristics/description are missing
