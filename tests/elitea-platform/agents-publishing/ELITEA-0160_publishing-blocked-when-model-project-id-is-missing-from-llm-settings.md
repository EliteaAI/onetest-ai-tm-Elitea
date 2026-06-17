---
id: ELITEA-0160
title: "Publishing blocked when model_project_id is missing from LLM settings after agent import"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [story:4049, story:4432, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4432]
---
# ELITEA-0160: Publishing blocked when model_project_id is missing from LLM settings after agent import

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify publishing is blocked with a clear error when `model_project_id` is missing from `llm_settings` — which happens after importing an agent between projects.

**Coverage:**
- Main agent with missing `model_project_id` → publish blocked with actionable error
- Sub-agent with missing `model_project_id` → publish blocked, sub-agent named in error

## Preconditions

- Logged into ELITEA with publish permissions
- An agent (with at least one sub-agent) has been imported from another project
- The model name appears to be set in LLM Settings but `model_project_id` is not resolved for the current project

## Test Data

| Variant | Entity | State |
|---------|--------|-------|
| A | Main agent | Imported; `llm_settings = {"model_name": "gpt-5.2"}` — no `model_project_id` |
| B | Sub-agent | Imported; same state as Variant A; main agent restored to valid shared model |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an imported agent where LLM Settings show a model name but the integration is broken/unresolved | Agent opens; LLM Settings may show the model name but integration source is missing |
| 2 | Variant A: Attempt to publish the agent as-is | Blocked with: "LLM model settings are incomplete for parent agent (missing model_project_id). Re-select the LLM model in the agent editor to update model settings before publishing." |
| 3 | Variant B: Re-select a valid shared Public model on the main agent; then attempt to publish (leaving sub-agent LLM unresolved) | Blocked with: "LLM model settings are incomplete for sub-agent '[name]' (missing model_project_id). Re-select the LLM model in the agent editor to update model settings before publishing." |
| 4 | Verify agent status in both variants | Agent remains unpublished |

## Expected Final State

Agent remains unpublished

## Pass/Fail Criteria

**Pass:**
- Publishing blocked in both variants
- Error names the affected entity (main agent or sub-agent) and instructs user to re-select the model

**Fail:**
- Publishing proceeds despite missing `model_project_id`
- Error is absent or does not identify the affected entity
