---
id: ELITEA-0158
title: "Publishing blocked when a project-specific (private) model is selected on main agent or sub-agent"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [story:4049, story:4432, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4432]
---
# ELITEA-0158: Publishing blocked when a project-specific (private) model is selected on main agent or sub-agent

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify publishing is blocked when a model from a private project integration is used — tested for the main agent and a sub-agent separately.

**Coverage:**
- Main agent using private model → "Model is project-specific (not a shared model)" error
- Sub-agent using private model → same error, sub-agent named explicitly
- Multiple sub-agent violations returned in a single batched response

## Preconditions

- Logged into ELITEA with publish permissions
- A private LLM integration already exists under the current project (not from Public) — e.g. own API key added in Settings → Integrations
- At least one sub-agent is configured on the main agent

## Test Data

| Variant | Entity | Model source |
|---------|--------|-------------|
| A | Main agent | Private project integration (not Public) |
| B | Sub-agent | Private project integration; main agent restored to valid shared Public model |
| C | Two sub-agents | Both with private model; main agent on valid shared Public model |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Variant A: Open the main agent → LLM Settings → select a model from the private project integration (not from the Public/shared section) → Save | Agent saved with non-public model |
| 2 | Attempt to publish | Blocked with: "Model '[model_name]' used by parent agent is project-specific (not a shared model). Only shared models from the Public project are allowed for publishing." |
| 3 | Variant B: Restore main agent to a valid shared Public model (e.g. gpt-5.2); open sub-agent → LLM Settings → select the private model → Save | Sub-agent saved with non-public model; main agent is valid |
| 4 | Attempt to publish | Blocked with: "Model '[model_name]' used by sub-agent '[name]' is project-specific (not a shared model). Only shared models from the Public project are allowed for publishing." |
| 5 | Variant C: Configure a second sub-agent also with a private model → Attempt to publish | Both sub-agent errors returned in a single response, separated by ' \| ' |
| 6 | Verify agent status in all variants | Agent remains unpublished |

## Expected Final State

Agent remains unpublished

## Pass/Fail Criteria

**Pass:**
- Publishing blocked in all variants
- Error names the model and the specific entity (main agent or sub-agent by name)
- Multiple sub-agent violations collected and returned in a single batched response

**Fail:**
- Publishing proceeds with a private model on any entity
- Errors reference wrong entity, or multiple violations are not batched
