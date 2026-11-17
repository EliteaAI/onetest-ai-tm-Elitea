---
id: ELITEA-4705
title: "Node Pickers — Project-wide Lists, Search, Create New, Lazy Loading and Warnings"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7159, EliteaAI/elitea_issues#7157]
---
# ELITEA-4705: Node Pickers — Project-wide Lists, Search, Create New, Lazy Loading and Warnings

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that node pickers (Agent, Toolkit, MCP, LLM Toolkits & MCPs) list everything in the project with correct type filtering, search, lazy loading, "In use" tags, "+ Create new" shortcuts, empty state and auth warnings.

**Coverage:**
- Agent picker: agents + pipelines; Toolkit picker: non-MCP only; MCP picker: MCP only; LLM: toolkits + MCPs (multi-select)
- Search; icon/name/description per row
- Lazy loading on large lists
- "In use" tag for items used in this pipeline
- + Create new (opens in a new tab; new item is not pre-selected on return — accepted)
- Empty state text
- MCP "Log in" warning; Toolkit has no inline auth warning (accepted)
- Known: elitea_issues#7397 (spurious "Agent not found" on switching)

## Preconditions

- Logged in to {{base_url}}
- Project A with 50+ toolkits, several MCPs (one requiring login), agents and pipelines
- Project B with no agents or pipelines

## Test Data

- None

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Add an Agent node; open its Agents & Pipelines picker. | Lists all agents **and** pipelines in the project (grouped), not only attached ones; search placeholder *"Search agents and pipelines..."*; each row shows icon, name, short description. |
| 2 | Add a Toolkit node; open its picker. | Lists all non-MCP toolkits; no MCPs. |
| 3 | Add an MCP node; open its picker. | Lists MCPs only. An MCP needing auth shows an inline **Log in** action. |
| 4 | Add an LLM node; open Toolkits & MCPs. | Multi-select listing toolkits and MCPs. |
| 5 | Type part of a name in each picker's search. | List filters to matching items. |
| 6 | In the Toolkit picker (50+ items), scroll to the bottom. | More items load after a short delay (lazy loading). |
| 7 | Select a toolkit in one node; open the Toolkit picker in a second Toolkit node. | The item is tagged **In use**. |
| 8 | Click **+ Create new agent** / **+ Create new pipeline** / **+ Create new** (toolkit/MCP). | The create flow opens in a new tab (`/app/agents/create`, `/app/pipelines/create`, …). On returning, the new item is not pre-selected — select it manually (accepted). |
| 9 | Switch an Agent node from one valid agent/pipeline to another. | No "Agent not found" warning is shown. Known: elitea_issues#7397 (intermittent false warning). |
| 10 | In Project B, open the Agent picker. | Empty state *"No agents or pipelines in this project yet"* with + Create new. |
| 11 | Open the Toolkit picker for a toolkit with broken credentials. | No inline auth warning in the picker (accepted difference from MCP). |
| 12 | Point an Agent node at a since-deleted agent (existing pipeline). | Warning *"Agent not found — select a replacement or delete this node"*. |

## Expected Final State

All node pickers list project-wide items with correct type filtering, search and lazy loading, mark used items, offer + Create new, and show the empty state / MCP login warning.

## Pass/Fail Criteria

**Pass:**
- Correct type filtering per picker; project-wide lists
- Search, lazy loading and "In use" tag work
- + Create new opens the create flow; empty state and MCP Log in shown

**Fail:**
- Picker shows only already-attached items, or mixes MCPs/toolkits incorrectly
- Search or lazy loading broken
- False "not found" warning on a valid selection
