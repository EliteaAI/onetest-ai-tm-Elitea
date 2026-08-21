---
id: ELITEA-2694
title: "Agent Toolkit Attachment Shows Correct (Chosen) Tool"
priority: high
type: functional
module: toolkits-credentials/group-tools-within-toolkit
status: ready
execution_type: manual
tags: [feat:toolkits, tools, agents, integration]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2694: Agent Toolkit Attachment Shows Correct (Chosen) Tool

**Module:** Toolkits Credentials / Group Tools Within Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that agents with attached toolkits correctly display tool information after the grouping changes.

**Coverage:**
- Agent displays correct tool selected in attached toolkit
- Tools section shows all selected tools
- Agent can successfully execute tools from the attached toolkit
- No regression in agent-toolkit integration

## Preconditions

- Logged in to {{base_url}}
- User has access to ELITEA platform
- An agent with an attached SDK toolkit exists (e.g., agent with GitHub toolkit)
- The attached toolkit has tools from multiple groups selected
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the toolkit attached to the agent and note which tools are selected: X Read, Y Create & update, Z Delete, W Execute (Total: X+Y+Z+W). | Tool selection state is documented. |
| 2 | Save toolkit if any changes were made. | Toolkit saves successfully (or no save needed). |
| 3 | Navigate to Agents page and open the agent that has this toolkit attached. | Agent configuration page opens. |
| 4 | Navigate to Agent details/configuration and locate the Tools section. | Tools section is visible. |
| 5 | Verify tool by clicking 'Show tools'. | Shown only tools which wrere selected in step 1. |
| 6 | Execute the agent with a prompt that would use one of the attached tools (e.g., "List my GitHub repositories"). | Agent processes the request. |
| 7 | Verify the tool executes successfully. | Tool execution **succeeds**. |
| 8 | Execute the agent with a prompt that would use one of the tools which wasn't selected in step 1 (e.g., "get issue #23"). | Agent answer with explanation thet he doesn't have such tool, e.g. "there’s no “get issue”/“list issues” capability".|

## Expected Final State

Agent correctly displays and executes tools from the attached toolkit.

## Pass/Fail Criteria

**Pass:**
- Agent displays correct tool count from attached toolkit
- Tools section shows all selected tools
- Agent can successfully execute tools from the attached toolkit
- No regression in agent-toolkit integration

**Fail:**
- Agent displays incorrect tool count
- Tools section shows wrong tools or missing tools
- Agent cannot execute tools from the attached toolkit
- Tool execution fails or returns incorrect results
