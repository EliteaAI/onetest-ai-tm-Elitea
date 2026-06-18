---
id: ELITEA-0165
title: "Subpipeline Attached to Agent Is Excluded From Code based and AI Validation"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:4162, story:4049, story:3774, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4525, EliteaAI/elitea_issues#4162]
---
# ELITEA-0165: Subpipeline Attached to Agent Is Excluded From Code based and AI Validation

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a subpipeline attached directly to an agent produces zero validation findings of any severity, while the agent's own sub-agents are still evaluated normally.

**Coverage:**
- Subpipeline content is not inspected by Code based and AI validation at any severity level
- Sub-agent attached to the same parent agent is still present in the validation scope
- Pipeline exclusion does not suppress all evaluation — the parent and sub-agent are still validated

## Preconditions

- Logged in to ELITEA as a regular user
- Environment: {{base_url}}
- Agent `TestAgent_A` has 1 direct subpipeline `Pipeline_1` (minimal/stub YAML) and 1 direct sub-agent `SubAgent_1` (valid instructions ≥100 chars)

## Test Data

- Agent: `TestAgent_A`
- Subpipeline: `Pipeline_1` (minimal/stub YAML)
- Sub-agent: `SubAgent_1` (valid instructions ≥100 chars)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open `TestAgent_A`. Confirm `Pipeline_1` and `SubAgent_1` are configured. Click **Publish** → **Continue**. | Validation runs and completes. |
| 2 | Review all validation results across all severity levels (Critical, Warning, Info). | Zero findings of any severity reference `Pipeline_1` or originate from its content. At least one validation entry exists for the parent agent or `SubAgent_1`, confirming included components were evaluated. |

## Expected Final State

Zero findings of any severity reference `Pipeline_1` or originate from its content. At least one validation entry exists for the parent agent or `SubAgent_1`, confirming included components were evaluated.

## Pass/Fail Criteria

**Pass:**
- 0 errors/warnings/suggestions from `Pipeline_1` or any pipeline content
- Validation output contains entries for the parent agent or `SubAgent_1` (pipeline exclusion did not suppress all evaluation)

**Fail:**
- Any finding of any severity references `Pipeline_1` or its YAML content
- Validation output is completely empty — nothing was evaluated at all
