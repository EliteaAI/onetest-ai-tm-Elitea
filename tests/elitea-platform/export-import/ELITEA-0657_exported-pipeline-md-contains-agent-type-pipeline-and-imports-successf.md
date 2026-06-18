---
id: ELITEA-0657
title: "Exported Pipeline MD Contains agent_type: pipeline and Imports Successfully"
priority: critical
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3726]
---
# ELITEA-0657: Exported Pipeline MD Contains agent_type: pipeline and Imports Successfully

**Module:** Export Import · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an exported Pipeline .md file contains agent_type: pipeline and that re-importing it recreates the pipeline correctly.

**Coverage:**
- agent_type: pipeline in exported frontmatter (not openai)
- Import Wizard identifies entity as Pipeline; import succeeds

## Preconditions

- Logged in to {{base_url}} Private project selected
- At least one Pipeline exists (no nested dependencies, single .md export); a destination project is accessible

## Test Data

- Any existing Pipeline (no nested dependencies, single .md export)
- Expected frontmatter field: agent_type: pipeline

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines. Open any Pipeline -> three-dot menu -> Export | .md file downloads |
| 2 | Open the file in a text editor. Locate agent_type in YAML frontmatter | Value is exactly: pipeline |
| 3 | Pipelines menu -> Import -> select the .md file | Import Wizard opens; left panel shows entity type Pipeline (not openai) |
| 4 | Select destination project -> click Import | Success notification; no errors |
| 5 | Navigate to Pipelines list in destination project | Imported pipeline present with correct name and configuration |

## Expected Final State

Imported pipeline present with correct name and configuration

## Pass/Fail Criteria

**Pass:** agent_type: pipeline in file; wizard shows "Pipeline"; import succeeds
**Fail:** agent_type: openai or any other value; import fails or entity type wrong
