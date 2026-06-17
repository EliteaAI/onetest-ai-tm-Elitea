---
id: ELITEA-0656
title: "Exported Agent MD Contains agent_type: agent and Imports Successfully"
priority: critical
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3726]
---
# ELITEA-0656: Exported Agent MD Contains agent_type: agent and Imports Successfully

**Module:** Export Import · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an exported Agent .md file contains agent_type: agent and that re-importing it recreates the agent correctly.

**Coverage:**
- agent_type: agent in exported frontmatter (not openai)
- Import Wizard identifies entity as Agent; import succeeds

## Preconditions

- Logged in to {{base_url}} Private project selected
- At least one Agent with a toolkit exists; a destination project is accessible

## Test Data

- Any existing Agent (no nested dependencies, single .md export)
- Expected frontmatter field: agent_type: agent

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents. Open any Agent -> three-dot menu -> Export | .md file downloads |
| 2 | Open the file in a text editor. Locate agent_type in YAML frontmatter | Value is exactly: agent |
| 3 | Agents menu -> Import -> select the .md file | Import Wizard opens; left panel shows entity type Agent (not openai) |
| 4 | Select destination project -> click Import | Success notification; no errors |
| 5 | Navigate to Agents list in destination project | Imported agent present with correct name and configuration |

## Expected Final State

Imported agent present with correct name and configuration

## Pass/Fail Criteria

**Pass:** agent_type: agent in file; wizard shows "Agent"; import succeeds
**Fail:** agent_type: openai or any other value; import fails or entity type wrong
