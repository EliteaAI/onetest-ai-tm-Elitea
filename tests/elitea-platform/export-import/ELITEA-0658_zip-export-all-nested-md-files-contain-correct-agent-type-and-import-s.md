---
id: ELITEA-0658
title: "ZIP Export — All Nested MD Files Contain Correct agent_type and Import Successfully"
priority: critical
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3726]
---
# ELITEA-0658: ZIP Export — All Nested MD Files Contain Correct agent_type and Import Successfully

**Module:** Export Import · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that for both Agents and Pipelines with nested dependencies, every .md file inside the exported ZIP contains the correct agent_type for its entity type, and that importing the ZIP recreates all entities correctly.

**Coverage:**
- No .md file in the ZIP contains agent_type: openai
- Each file's agent_type matches its entity type (agent or pipeline)
- ZIP import completes; all nested entities appear in correct menus

## Preconditions

- Logged in to {{base_url}} Private project selected
- An Agent with ≥1 nested sub-agent exists
- A Pipeline with ≥1 nested sub-pipeline or agent exists
- Local filesystem accessible to extract ZIPs; a destination project is accessible

## Test Data

Parameter A: Agent with ≥1 nested sub-agent → agent_type: agent for all agent files; agent_type: pipeline for any nested pipeline files
Parameter B: Pipeline with ≥1 nested sub-pipeline or agent → agent_type: pipeline for all pipeline files; agent_type: agent for any nested agent files

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open entity (Agent for Parameter A / Pipeline for Parameter B) → ⋮ → Export | .zip file downloads |
| 2 | Extract ZIP. For each .md file check agent_type in YAML frontmatter | Every Agent .md = agent_type: agent; every Pipeline .md = agent_type: pipeline; zero files contain agent_type: openai |
| 3 | Navigate to correct menu (Agents for A / Pipelines for B) → Import → select .zip | Import Wizard opens and shows all entities from archive |
| 4 | Select destination project → click Import | Import completes; success notification; no errors |
| 5 | Verify root entity and all nested entities in destination project under correct menus | All entities created correctly under their respective sections (Agents or Pipelines) |

## Expected Final State

All entities created correctly under their respective sections (Agents or Pipelines)

## Pass/Fail Criteria

**Pass:** Zero agent_type: openai in any file; all entity types correct per parameter row; import recreates all entities
**Fail:** Any file still has agent_type: openai; import fails; any entity missing or in wrong section
