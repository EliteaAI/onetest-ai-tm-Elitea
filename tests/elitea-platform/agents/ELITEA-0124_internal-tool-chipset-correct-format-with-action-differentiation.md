---
id: ELITEA-0124
title: "Internal Tool Chipset — Correct Format with Action Differentiation"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [nfr:usability, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3535]
---
# ELITEA-0124: Internal Tool Chipset — Correct Format with Action Differentiation

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify internal tools display as [Icon] ToolName: actionName without redundant prefixes, and that multiple actions from the same tool are distinguishable.

**Coverage:**
- Attachments chipsets show "Attachments: createFile" and "Attachments: readFile" — no "Internal:" or "Tool:" prefix
- Planner chipsets show "Planner: start_step" and "Planner: complete_step" — no redundant prefix
- Different actions from the same tool produce distinct, readable chipset entries
- Zero chipsets in the trace contain any "Internal:", "Tool:", or "InternalTool:" prefix

## Preconditions

- Logged in to ELITEA at {{base_url}}
- An Agent exists with both Attachments and Planner internal tools enabled
- Agent workflow is capable of triggering multiple internal tool actions (createFile, readFile, start_step, complete_step)
- User has access to the agent's execution trace panel
- Browser: Chrome/Edge latest

## Test Data

- Internal tools: Attachments (actions: createFile, readFile), Planner (actions: start_step, complete_step)
- Test prompt: "Create a file named notes.txt, write content to it, read it back, then plan the next steps"
- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA. In the left sidebar, click Agents and open the target agent. | Agent detail page loads. |
| 2 | Navigate to the agent's Settings / Toolkits section. Confirm that both Attachments and Planner internal tools are listed as enabled. | Both Attachments and Planner appear in the enabled tools list. |
| 3 | Switch to the Chat or Run tab within the agent. | Chat input is available. |
| 4 | Enter a prompt that requires file operations and planning (e.g., 'Create a file named notes.txt, write content to it, read it back, then plan the next steps'). Press Send. | Agent begins processing; multiple tool calls are expected. |
| 5 | Wait for the full response. Locate the thinking steps / execution trace panel. | Execution trace shows multiple chipsets for different tool actions. |
| 6 | Scan the execution trace for chipsets related to Attachments. Locate one for createFile. Read the full label including any prefix. | Chipset label reads 'Attachments: createFile' with the Attachments icon — no 'Internal:' or 'Tool:' prefix before it. |
| 7 | Locate the Attachments chipset for readFile (a different action). Read its label. | Chipset label reads 'Attachments: readFile' — the action name makes it visually distinct from the createFile chipset. |
| 8 | Scan the execution trace for Planner chipsets. Locate start_step. Read the full label. | Chipset label reads 'Planner: start_step' with the Planner icon — no 'Internal:' or 'Tool:' prefix. |
| 9 | Locate the Planner chipset for complete_step. Read its label and compare to start_step. | Chipset label reads 'Planner: complete_step' — different from start_step; each action is a distinct, distinguishable entry. |
| 10 | Review all visible chipsets in the trace. Confirm none starts with a prefix like 'Internal:', 'Tool:', or 'InternalTool:'. | Zero chipsets contain any redundant prefix before the tool name. |

## Expected Final State

Zero chipsets contain any redundant prefix before the tool name.

## Pass/Fail Criteria

**Pass:**
- Each internal tool chipset follows [Icon] ToolName: actionName format
- No redundant prefix (Internal:, Tool:, InternalTool:) present on any chipset
- Different actions from the same tool (e.g., createFile vs readFile) are visually distinct entries

**Fail:**
- Any chipset shows a redundant prefix before the tool name
- Two actions from the same tool appear identical (indistinguishable)
