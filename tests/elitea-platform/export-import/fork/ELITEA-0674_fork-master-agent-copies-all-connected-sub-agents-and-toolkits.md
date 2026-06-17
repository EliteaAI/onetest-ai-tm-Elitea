---
id: ELITEA-0674
title: "Fork Master Agent Copies All Connected Sub-Agents and Toolkits"
priority: high
type: functional
module: fork
status: ready
execution_type: manual
tags: [feat:import-forking, story:3728, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3728]
---
# ELITEA-0674: Fork Master Agent Copies All Connected Sub-Agents and Toolkits

**Module:** Fork · **Priority:** High · **Type:** Functional

**Objective:** Verify that forking a master agent with sub-agents or prompts configured as toolkits copies all directly connected entities to the target project in a single operation.

**Coverage:**
- Recursive fork of master agent with connected entities
- Toolkit references in forked agent point to newly forked sub-entities (not originals)
- Single-operation completeness

## Preconditions

- Logged in as Editor in Source Project and Target Project
- Source Project has a master agent with at least one sub-agent or prompt configured as a toolkit

## Test Data

- Master agent name: noted before fork
- Connected sub-agent/prompt names: noted before fork

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Source Project → Agents, identify and note a master agent and its connected sub-agent/prompt toolkit names | Names recorded |
| 2 | Open the master agent → click Fork | Fork wizard opens |
| 3 | Inspect the wizard preview — verify all connected entities appear in the selection | Sub-agents/prompts are listed in the wizard |
| 4 | Select Target Project → click Fork | Fork completes |
| 5 | Navigate to Target Project → Agents | Master agent is present |
| 6 | Open master agent → navigate to toolkit configuration | Toolkits are listed |
| 7 | Verify toolkit references point to the newly forked sub-entities in the Target Project (not the source project originals) | Toolkit references show Target Project entity IDs/links |
| 8 | Confirm sub-agents/prompts also appear independently in Target Project → Agents | Sub-agents/prompts are present as standalone entities in Target Project |

## Expected Final State

Sub-agents/prompts are present as standalone entities in Target Project

## Pass/Fail Criteria

**Pass:**
- All connected sub-agents/prompts forked to Target Project
- Toolkit configuration references the newly forked entities (not sources)
- All entities accessible and functional in Target Project

**Fail:**
- Sub-agents/prompts are not created in Target Project
- Toolkit configuration still references the Source Project entities
- Master agent toolkit configuration is empty or broken after fork
