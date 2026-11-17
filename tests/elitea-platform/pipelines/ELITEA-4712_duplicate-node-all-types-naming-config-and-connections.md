---
id: ELITEA-4712
title: "Duplicate Node — All Node Types: Naming, Copied Configuration and Cleared Connections"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7161]
---
# ELITEA-4712: Duplicate Node — All Node Types: Naming, Copied Configuration and Cleared Connections

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify Duplicate for every addable node type: button and tooltip, naming (`_copy`, `_copy_2`), placement, identical configuration (Flow and YAML) except `id` and connection keys, cleared connections and entry point, toast, auto-opened panel, Save/Discard, single attachment, run from the copy, and unavailable states.

**Coverage:**
- Duplicate icon next to Edit with AI and Delete; tooltip "Duplicate node"
- `_copy`, `_copy_2`, … ; original position unchanged; copy placed next to it (partial overlap accepted)
- Configuration identical in Flow and YAML, incl. agent/version, toolkit/MCP + tools, LLM tools, conditions, descriptions, YAML-only keys
- Connections cleared per type; not entry point; not in interrupt lists; others not rewired
- Toast, panel opens, Save enabled, Discard removes, persists after Save
- No second attachment; copy runs and is highlighted (elitea_issues#7418 fixed)
- Disabled for deprecated types; no End duplicate; no multi-select/copy-paste/Ctrl+D
- See ELITEA-4719 for the main E2E flow

## Preconditions

- Logged in to {{base_url}}
- A pipeline with all 10 node types fully configured and connected: Router with routes + default output, Decision with outputs + default output, HITL with approve/edit/reject routes, Agent as entry point, a YAML-only key on one node, `interrupt_before` on one node
- An existing pipeline with a deprecated node

## Test Data

- None

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open any node's panel; hover the footer icons. | Duplicate icon next to Edit with AI and Delete; tooltip *"Duplicate node"*. |
| 2 | Duplicate the Agent node. | Toast *"Agent 1 duplicated as Agent 1_copy"*; copy selected and its panel opens; Save enabled. |
| 3 | Observe placement. | Copy next to the original, offset down-right (partial overlap accepted); original position unchanged. |
| 4 | Duplicate the original Agent again. | New copy is named `Agent 1_copy_2`. |
| 5 | Compare Flow fields of the original and the copy. | Identical (agent/pipeline + version, task, input, output). |
| 6 | Repeat duplication for each of the other 9 types and diff node YAML original vs. copy. | Identical except `id` and connection keys, for every type: MCP/Toolkit `toolkit_name`, `tool`, `input_mapping`; LLM `tool_names` and prompts; Router `condition`; Decision `description` — formatting preserved. |
| 7 | Check connection keys on the copies. | No `transition`; Router `routes: []`, `default_output: ''`; Decision `nodes: []`, `default_output: ''`; HITL approve/edit/reject `''`. |
| 8 | Check the copy of the entry node and the node with `interrupt_before`. | Copy is not the entry point (no Trigger, no Entrypoint badge) and is not added to `interrupt_before/after`. |
| 9 | Check other nodes' connections. | Unchanged; nothing points to a `_copy` node. |
| 10 | Check the YAML-only key on the copied node. | Kept on the copy. |
| 11 | Observe TOOLS. | No second attachment for duplicated toolkit/MCP/agent nodes. |
| 12 | Click page-level **Discard**. | All unsaved copies removed. |
| 13 | Duplicate a node, leave it unconnected, Save, reload. | Copy persists; an unconnected copy is auto-connected to End. |
| 14 | Duplicate the MCP node; make the copy the entry point; connect it; Save; run. | Run succeeds; the **copy** is highlighted as running; thinking steps attribute the tool call to the copy (e.g. `test-github-mcp: get_me (MCP 1_copy)`). |
| 15 | Open the deprecated node's panel; hover Duplicate. | Disabled; tooltip *"Deprecated nodes can't be duplicated"*. |
| 16 | Select End; try multi-select, Ctrl/Cmd+C / V and Ctrl/Cmd+D. | End has no panel (nothing to duplicate); no multi-select duplicate, copy/paste or Ctrl/Cmd+D shortcut. |

## Expected Final State

Every addable node type can be duplicated into a disconnected, identically configured copy with the correct name, sharing the same attachment, and the copy runs and highlights correctly.

## Pass/Fail Criteria

**Pass:**
- Naming, toast, panel open, Save/Discard and persistence as specified
- Configuration identical except `id` and connection keys, for all 10 types
- Connections, entry point and interrupts not copied; others not rewired
- Single attachment; copy runs and is highlighted
- Disabled for deprecated types

**Fail:**
- Any configuration drift or leaked connection
- Copy becomes entry point or is rewired into the flow
- Second attachment created
- Run highlight on the wrong node
