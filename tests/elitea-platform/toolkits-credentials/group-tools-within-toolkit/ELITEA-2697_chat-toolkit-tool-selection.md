---
id: ELITEA-2697
title: "Chat Toolkit Tool Selection with Grouping"
priority: high
type: functional
module: toolkits-credentials/group-tools-within-toolkit
status: ready
execution_type: manual
tags: [feat:toolkits, tools, chat, integration]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2697: Chat Toolkit Tool Selection with Grouping

**Module:** Toolkits Credentials / Group Tools Within Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that attaching a toolkit in chat displays grouped tools correctly, allows tool selection changes, and executes only selected tools.

**Coverage:**
- Toolkit attachment via + Toolkits button works
- Right panel shows grouped tools matching toolkit configuration
- Tool selection changes can be saved from chat
- Selected tools execute correctly
- Unselected tools are not available for execution

## Preconditions

- Logged in to {{base_url}}
- User has access to ELITEA platform
- A configured SDK toolkit exists with tools from multiple groups (some selected, some not)
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a chat session. | Chat interface opens. |
| 2 | Click on **+ Toolkits** button and select a configured SDK toolkit (e.g., GitHub). | Toolkit is attached to the chat. Toolkit appears in the chat participants. |
| 3 | On the right panel, click on the attached toolkit to expand it. View the selected tools. | Tools are displayed **grouped** (Read, Create & update, Delete, Execute). Only **selected tools** from the toolkit configuration are shown as active. |
| 4 | Select additional tools that were not previously selected (e.g., add a tool from Create & update group). Click **Save**. | New tools are added to the selection. Save completes successfully. |
| 5 | Send a prompt that would trigger the **newly added tool** (e.g., "Create a new issue titled 'Test issue'"). | Agent uses the newly added tool. Tool execution **succeeds** with correct results. |
| 6 | Send a prompt that would trigger one of the **originally selected tools** (e.g., "List open issues" or "Get repository info"). | Agent uses the originally selected tool. Tool execution **succeeds** with correct results. |
| 7 | Send a prompt that would require a **tool that is NOT selected** in the toolkit configuration (e.g., "Delete issue #123" when delete tool is not selected). | Agent responds that it **doesn't have such tool/capability** in its configuration. Tool is not executed. |

## Expected Final State

Chat correctly displays grouped tools, allows selection changes, and respects tool availability.

## Pass/Fail Criteria

**Pass:**
- Toolkit attaches via + Toolkits button
- Right panel shows tools grouped correctly (Read, Create & update, Delete, Execute)
- Tool selection changes save successfully
- Newly added tools execute correctly
- Originally selected tools continue to work
- Unselected tools are not available (agent reports no such capability)

**Fail:**
- Toolkit does not attach or display in chat
- Tools are not grouped in the right panel
- Tool selection changes do not save
- Selected tools fail to execute
- Unselected tools are executed (should not happen)
