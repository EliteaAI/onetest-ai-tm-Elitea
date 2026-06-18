---
id: ELITEA-1151
title: "get_pull_request tool works in Chat with ADO toolkit"
priority: medium
type: functional
module: ado-toolkit
status: ready
execution_type: manual
tags: [int:ado-repos, feat:toolkits, eng:backend, issue:4497, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4497]
---
# ELITEA-1151: get_pull_request tool works in Chat with ADO toolkit

**Module:** Ado Toolkit · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that Chat conversations using an agent with ADO toolkit can retrieve PR descriptions and display them correctly without UI rendering issues.

**Coverage:**
- Chat using agent with ADO toolkit can retrieve PR description
- Description content is properly displayed in chat response
- No UI rendering issues with description content
- Chat experience is smooth and functional

## Preconditions

- User authenticated with valid account
- Agent configured with ADO Toolkit
- Test ADO repository accessible with PRs
- Environment: {{base_url}}

## Test Data

- Agent name: [Agent with ADO Toolkit]
- Toolkit: ADO Toolkit
- Tool: get_pull_request
- PR ID: [Valid PR ID with description containing markdown, special chars]
- Expected chat behavior: Agent retrieves and displays description

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from sidebar | Chat page loads |
| 2 | Start a new conversation | New conversation started |
| 3 | Add an agent configured with ADO Toolkit | Agent added |
| 4 | Send a prompt: "Get PR #[ID] details including the description" | Prompt sent |
| 5 | Wait for agent to execute get_pull_request tool | Tool executes |
| 6 | Review the chat response | Response displayed |
| 7 | Verify agent includes PR description content in response | Description included |
| 8 | Verify markdown content renders correctly (or is displayed as-is based on design) | Markdown handled correctly |
| 9 | Verify special characters display correctly | Characters display correctly |
| 10 | Verify multi-line descriptions are formatted properly in chat | Formatting correct |
| 11 | Verify no UI rendering issues (truncation, overlap, formatting errors) | No rendering issues |
| 12 | Verify chat remains responsive and functional | Chat responsive |

## Expected Final State

Chat responsive

## Pass/Fail Criteria

**Pass:**
- Agent successfully retrieves PR description
- Description content is displayed in chat response
- Multi-line text is formatted properly
- Special characters and markdown display correctly
- No UI rendering issues
- Chat experience is smooth

**Fail:**
- Agent fails to retrieve description
- Description is not displayed in chat
- UI rendering issues appear (truncation, overlap, broken layout)
- Special characters are corrupted
- Chat becomes unresponsive or errors appear
- Markdown rendering causes UI issues
