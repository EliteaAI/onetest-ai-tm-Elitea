---
id: ELITEA-0143
title: "Agent with Toolkits"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.agents.test_agent_with_github_toolkit.TestAddToolkitToAgent.test_add_toolkit_to_agent
  - tests.ui.agents.test_agent_with_github_toolkit.TestChatWithAgentToolkit.test_agent_chat_with_github_toolkit
  - tests.ui.agents.test_agent_with_github_toolkit.TestRemoveToolkitFromAgent.test_remove_toolkit_from_agent
  - tests.ui.chat.test_agent_with_toolkit_chat.TestAgentWithToolkitInChat.test_agent_with_toolkit_executes_in_chat
tags: []
requirements: []
---
# ELITEA-0143: Agent with Toolkits

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can add toolkits to agents, use them in chat, and remove them when needed.

## Preconditions

- User logged into Elitea
- GitHub toolkit exists
- Test agent exists

## Test Data

- URL: {{base_url}}
- Test query: Search for Python repos

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Open agent configuration | Toolkits section visible |
| ? | Add GitHub toolkit to agent | Toolkit appears in agent's toolkit list |
| ? | Start chat with agent, ask GitHub-related question | Agent uses toolkit, provides GitHub data |
| ? | Remove toolkit from agent | Toolkit removed from list |

## Expected Final State

Toolkit removed from list

## Pass/Fail Criteria

**Pass:**
- Toolkit added to agent
- Agent uses toolkit in chat
- Toolkit removed successfully

**Fail:**
- Toolkit not available in agent
- Chat doesn't use toolkit
- Remove fails
