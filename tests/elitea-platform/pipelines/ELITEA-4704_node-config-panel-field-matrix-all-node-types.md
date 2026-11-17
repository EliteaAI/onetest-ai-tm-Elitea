---
id: ELITEA-4704
title: "Node Configuration Panel — Field Matrix and Card Summary for All Node Types"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7157, EliteaAI/elitea_issues#7156]
---
# ELITEA-4704: Node Configuration Panel — Field Matrix and Card Summary for All Node Types

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that each of the 10 node types shows exactly its specified Basic and Advanced fields in the node configuration panel, that the Trigger field appears only on the entry-point node, and that each card's summary reflects its configuration.

**Coverage:**
- Basic/Advanced fields per type (10 types)
- Trigger as first Basic field on the entry node only; Webhook option; schedules hint
- Selects for nodes vs. state variables
- Card summary per type before/after configuration
- Deprecated types show the Deprecated badge
- Field-level AI Assistant where applicable

## Preconditions

- Logged in to {{base_url}}
- A pipeline with one node of each of the 10 types; project has at least one agent, toolkit and MCP

## Test Data

| Type | Basic | Advanced |
|------|-------|----------|
| Agent | Agents & Pipelines (searchable, + Create new agent / + Create new pipeline), Version, Task (Type + Value) | Input, Output |
| Code | Code (Type: Fixed + Value) | Input, Output, Structured output |
| Decision | Decision criteria, Decision outputs, Default output | Input |
| Human-in-the-loop | User message (Type + Value), Approve, Edit, Edit state key, Reject (default END) | Input |
| LLM | Toolkits & MCPs, System (Type + Value), Task (Type + Value) | Input, Output, Chat history, Structured output |
| MCP | MCP select (then Tool + input mapping) | Input, Output, Structured output |
| Printer | Printer (Type + Value), Final message | — (no Advanced section) |
| Router | Condition, Routes, Default output | Input |
| State modifier | Jinja Template, Variables to clean | Input, Output |
| Toolkit | Toolkit select (then Tool + input mapping) | Input, Output, Structured output |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the entry-point node's panel. | **Trigger** is the first Basic field (default *Chat message*, option *Webhook*), with hint *"To run this pipeline on a timer, use the schedules section."* |
| 2 | Open a non-entry node's panel. | No Trigger field. |
| 3 | For each of the 10 types, open the panel and compare Basic and Advanced with Test Data. | Each type shows exactly its listed fields with the listed labels (e.g. "Decision criteria", not "Description"). Printer has no Advanced section. |
| 4 | Decision / Router / HITL: open their output/route selects. | They list **nodes**, not state variables. |
| 5 | Agent: select an agent. | Selected name shows in the select with an ✕ to clear; Version select and Task (Fixed / F-String / Variable, info *"Task for agent"*, value hint *"Value of string type is expected"*) appear. |
| 6 | Toolkit / MCP: select a toolkit/MCP, then a tool. | Tool select appears, then the tool's required/optional input-mapping rows. |
| 7 | For each type, observe the card before and after configuring. | Before: **Not configured**. After: a type-specific summary (e.g. Agent: agent name + task preview; Toolkit/MCP: toolkit › tool + "Params N/N set"; Code: first code line). |
| 8 | Use the field-level AI Assistant on Code and Printer. | It changes the field value as before. |
| 9 | Open an existing pipeline with a deprecated node (Condition / Function). | Deprecated badge + "⚠ Deprecated" text shown; panel opens. |
| 10 | Select Webhook in the Trigger dropdown. | The existing webhook setup modal opens unchanged. |

## Expected Final State

Every node type exposes exactly its specified Basic/Advanced fields in the panel, Trigger appears only on the entry node, and card summaries reflect configuration.

## Pass/Fail Criteria

**Pass:**
- All 10 types match the field matrix exactly
- Trigger only on the entry node
- Node selects list nodes; Not configured → summary transition works per type

**Fail:**
- Any missing, extra or mislabelled field
- Trigger on a non-entry node
- Card summary not updated after configuration
