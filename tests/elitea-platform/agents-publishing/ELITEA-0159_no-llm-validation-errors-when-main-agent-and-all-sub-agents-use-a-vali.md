---
id: ELITEA-0159
title: "No LLM validation errors when main agent and all sub-agents use a valid shared Public model"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [story:4049, story:4432, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4432]
---
# ELITEA-0159: No LLM validation errors when main agent and all sub-agents use a valid shared Public model

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that no LLM-related validation errors are returned when the main agent and all sub-agents use a valid shared model from the Public project.

**Coverage:**
- All three LLM checks pass for every entity in the agent tree
- No false-positive LLM errors on a correctly configured agent

## Preconditions

- Logged into ELITEA with publish permissions
- At least one shared Public model is available (e.g. gpt-5.2)
- Main agent and all sub-agents configured with a Public shared model
- All other required fields valid (name, description, tags, instructions)

## Test Data

| Entity | Model |
|--------|-------|
| Main agent | gpt-5.2 (or any available Public/shared model) |
| Each sub-agent | Any Public/shared model |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open main agent → LLM Settings → select a model from the Public/shared section (e.g. gpt-5.2) → Save | Main agent LLM shows shared model selected |
| 2 | Open each sub-agent → LLM Settings → select a Public shared model → Save | All sub-agents have valid shared Public models |
| 3 | Attempt to publish the agent | Publish validation runs across main agent and all sub-agents |
| 4 | Check the validation result for any LLM-related errors | No errors containing "LLM", "model", "llm_settings", or "shared" are returned |
| 5 | Observe publishing outcome | Agent publishes (or is blocked only by unrelated validation checks — not LLM) |

## Expected Final State

Agent publishes (or is blocked only by unrelated validation checks — not LLM)

## Pass/Fail Criteria

**Pass:**
- Zero LLM-related validation errors returned for any entity
- Publishing not blocked at the LLM validation step

**Fail:**
- False-positive LLM error raised for a correctly configured shared Public model on the main agent or any sub-agent
