---
id: ELITEA-1153
title: "get_pull_request tool works in Agent with ADO toolkit"
priority: high
type: functional
module: ado-toolkit
status: ready
execution_type: manual
tags: [int:ado-repos, feat:toolkits, eng:backend, issue:4497, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4497]
---
# ELITEA-1153: get_pull_request tool works in Agent with ADO toolkit

**Module:** Ado Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that an Agent configured with ADO toolkit can successfully call get_pull_request and access the description field.

**Coverage:**
- Agent configured with ADO toolkit can call get_pull_request
- Description field is returned and accessible to agent
- Agent can process and use description field content
- Agent execution completes without errors

## Preconditions

- User authenticated with valid account
- ADO Toolkit configured and available
- Agent created with ADO toolkit attached
- Test ADO repository accessible with PRs
- Environment: {{base_url}}

## Test Data

- Agent name: [Test Agent with ADO Toolkit]
- Toolkit: ADO Toolkit
- Tool: get_pull_request
- PR ID: [Valid PR ID with description]
- Agent instructions: Include instructions to retrieve PR details using get_pull_request

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents from sidebar | Agents page loads |
| 2 | Create or open an agent configured with ADO Toolkit | Agent opens |
| 3 | Ensure agent instructions include guidance to use get_pull_request when asked about PR details | Instructions set |
| 4 | Save the agent | Agent saved |
| 5 | Navigate to Chat from sidebar | Chat opens |
| 6 | Start a new conversation | New conversation started |
| 7 | Add the agent to the chat | Agent added |
| 8 | Send a prompt: "Get details for PR #[ID] including the description" | Prompt sent |
| 9 | Wait for agent to execute get_pull_request tool | Tool executes |
| 10 | Verify agent response includes PR description content | Description included |
| 11 | Verify agent can reference or summarize the description field | Agent processes description |
| 12 | Verify execution completes without errors | No errors |

## Expected Final State

No errors

## Pass/Fail Criteria

**Pass:**
- Agent executes get_pull_request successfully
- Description field is retrieved by the agent
- Agent response includes or references description content
- No execution errors or warnings
- Agent can process description field data

**Fail:**
- Agent fails to execute get_pull_request
- Description field is not retrieved
- Agent response does not include description
- Execution errors appear
- Agent cannot access description field
