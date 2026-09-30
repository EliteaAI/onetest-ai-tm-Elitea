---
id: ELITEA-3520
title: "Default (Empty) Tool Selection Exposes All 12 Actions"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3520: Default (Empty) Tool Selection Exposes All 12 Actions

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when `selected_tools` is left empty at toolkit creation, all 12 Outlook tools are exposed to the agent (empty selection = all tools, per SDK default).

## Preconditions

- An authorized Outlook credential exists

## Test Data

- Toolkit: `outlook-toolkit-default-tools`, `selected_tools` left empty/untouched

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a toolkit with a valid Outlook credential and leave the TOOLS section untouched (no explicit selection) | Toolkit is saved with empty `selected_tools` |
| 2 | Assign the toolkit to an agent and inspect the agent's available tool list (or ask the agent to list its Outlook capabilities) | All 12 tools are available: `list_messages`, `get_message`, `send_mail`, `reply_to_message`, `mark_as_read`, `list_folders`, `move_message`, `delete_message`, `search_messages`, `check_new_messages`, `find_new_messages`, `get_thread_messages` |

## Expected Final State

The agent has access to all 12 Outlook tools without any explicit tool selection having been made.

## Pass/Fail Criteria

**Pass:**
- All 12 documented tools are available when `selected_tools` is empty

**Fail:**
- One or more tools is missing with an empty selection
- Empty selection results in zero tools being exposed
