---
id: ELITEA-0163
title: "Subpipeline Attached to a Sub-Agent Is Excluded From AI Validation"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:4162, story:4049, story:3774, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4525, EliteaAI/elitea_issues#4162]
---
# ELITEA-0163: Subpipeline Attached to a Sub-Agent Is Excluded From AI Validation

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a subpipeline belonging to a sub-agent produces zero validation findings of any severity, while the sub-agent itself remains in the validation scope and is evaluated normally.

**Coverage:**
- Sub-agent's own subpipeline is excluded from AI validation
- Sub-agent is NOT excluded alongside its pipeline — it still appears in validation scope
- Pipeline exclusion does not propagate upward to suppress the owning sub-agent

## Preconditions

- Logged in to ELITEA as a regular user
- Environment: {{base_url}}
- Agent `TestAgent_C` has 1 direct sub-agent `ChildAgent` (valid instructions ≥100 chars)
- `ChildAgent` has its own subpipeline `ChildAgent_Pipeline` (minimal/stub YAML)

## Test Data

- Agent: `TestAgent_C`
- Sub-agent: `ChildAgent` (valid instructions ≥100 chars)
- Sub-agent's subpipeline: `ChildAgent_Pipeline` (minimal/stub YAML)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open `TestAgent_C`. Confirm `ChildAgent` is a direct sub-agent and `ChildAgent_Pipeline` belongs to `ChildAgent` (not to the parent). Click **Publish** → **Continue**. | Validation runs and completes. |
| 2 | Review all validation results across all severity levels (Critical, Warning, Info). | Zero findings of any severity reference `ChildAgent_Pipeline` or its content. At least one validation entry exists for `ChildAgent` (the sub-agent itself was not excluded along with its pipeline). |

## Expected Final State

Zero findings of any severity reference `ChildAgent_Pipeline` or its content. At least one validation entry exists for `ChildAgent` (the sub-agent itself was not excluded along with its pipeline).

## Pass/Fail Criteria

**Pass:**
- 0 errors/warnings/suggestions from `ChildAgent_Pipeline`
- At least one validation entry for `ChildAgent` is present (sub-agent evaluated normally)

**Fail:**
- Any finding of any severity references `ChildAgent_Pipeline`
- `ChildAgent` produces no validation output at all — incorrectly excluded because it has a pipeline attached
