---
id: ELITEA-0672
title: "Fork Preserves Agent Version Configuration Intact (Name, System Prompt, LLM Model, Tools)"
priority: high
type: functional
module: fork
status: ready
execution_type: manual
tags: [feat:import-forking, story:3728, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3728]
---
# ELITEA-0672: Fork Preserves Agent Version Configuration Intact (Name, System Prompt, LLM Model, Tools)

**Module:** Fork · **Priority:** High · **Type:** Functional

**Objective:** Verify that the forked agent version in the target project has identical name, description, system prompt, LLM model, and tools configuration as the source version (excluding credentials).

**Coverage:**
- Configuration fidelity: name, description, system prompt, LLM model, tools
- No data loss or corruption during fork
- Credential fields correctly blank

## Preconditions

- Logged in as Editor in Source Project and Target Project
- Source agent version has a complete configuration (all fields populated)

## Test Data

- Record before fork: agent name, version name, system prompt text, LLM model name, tool/toolkit list

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the source agent version → record: name, description, system prompt, LLM model, tools list | Values recorded |
| 2 | Fork the agent to Target Project | Fork completes |
| 3 | Navigate to Target Project → open the forked agent → open the forked version | Version detail opens |
| 4 | Compare agent name | Matches source |
| 5 | Compare system prompt text | Matches source exactly |
| 6 | Compare LLM model selection | Same model selected |
| 7 | Compare tools/toolkit list | Same tools listed (credentials blank) |
| 8 | Check description | Matches source |

## Expected Final State

Matches source

## Pass/Fail Criteria

**Pass:**
- All non-credential fields (name, system prompt, LLM model, tools) match source exactly
- Credential fields are blank

**Fail:**
- Any non-credential field is missing, truncated, or altered
- Tools configuration is empty or broken
- LLM model defaulted to a different model
