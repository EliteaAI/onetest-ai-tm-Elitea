---
id: ELITEA-3521
title: "Narrowing selected_tools Actually Restricts What the Agent Can Call"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3521: Narrowing selected_tools Actually Restricts What the Agent Can Call

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that explicitly selecting a subset of tools (e.g. only `list_messages` and `get_message`) prevents the agent from invoking any tool outside that subset.

## Preconditions

- An authorized Outlook credential exists

## Test Data

- Toolkit: `outlook-toolkit-narrow`, `selected_tools = [list_messages, get_message]`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a toolkit and enable only "List messages" and "Get message" in the TOOLS section | Only these two tools are checked |
| 2 | Save and assign the toolkit to an agent | Toolkit saved with 2 selected tools |
| 3 | In agent chat, ask the agent to send an email (`send_mail`) or delete a message (`delete_message`) | Agent reports it has no such capability / tool is not available — the call is not exposed to the model |
| 4 | Ask the agent to list messages | `list_messages` executes successfully |

## Expected Final State

Only the two selected tools are callable by the agent; all others are absent from its tool list.

## Pass/Fail Criteria

**Pass:**
- Agent can only invoke the explicitly selected tools
- Non-selected tools are not exposed/callable

**Fail:**
- Agent can invoke a tool outside the selected subset
- Selected tools are not available despite being enabled
