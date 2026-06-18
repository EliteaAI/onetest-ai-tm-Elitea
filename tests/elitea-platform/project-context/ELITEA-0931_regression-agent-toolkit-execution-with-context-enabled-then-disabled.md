---
id: ELITEA-0931
title: "Regression — Agent Toolkit Execution With Context Enabled then Disabled"
priority: medium
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, regression, story:3395, r-2.0.4, agents]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0931: Regression — Agent Toolkit Execution With Context Enabled then Disabled

**Module:** Project Context · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that enabling then disabling Project Context does not break agent toolkit execution or corrupt conversation history.

**Coverage:**
- Agent with toolkit works correctly with context enabled
- Agent with Ignore=ON executes normally
- Conversation history not corrupted
- All agents work correctly after context is disabled

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 2 | Enable Project Context. Run an agent that uses a toolkit (e.g. GitHub or Jira). Execute a tool call. | Toolkit executes correctly. No errors caused by context injection. |
| 3 | Run an agent with 'Ignore Project Context' = ON from the Agent page. | Agent executes normally. No errors. |
| 4 | Run a multi-turn conversation (3–4 turns) with an agent. Check the conversation history. | All messages present and correct. No duplicated or missing messages. |
| 5 | Disable the Project Context toggle. Run the same agents again. | All agents execute correctly with context disabled. No regressions introduced. |

## Expected Final State

All agents execute correctly with context disabled. No regressions introduced.

## Pass/Fail Criteria

**Pass:**
- Toolkit calls succeed with context enabled
- Conversation history is clean
- Agents work normally after context disabled

**Fail:**
- Toolkit errors occur only after enabling context
- Conversation messages are duplicated or missing
- Agents fail after toggling context off
