---
id: ELITEA-0164
title: "Components Nested Inside a Subpipeline Are Excluded From AI Validation"
priority: high
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:4162, story:4049, story:3774, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4525, EliteaAI/elitea_issues#4162]
---
# ELITEA-0164: Components Nested Inside a Subpipeline Are Excluded From AI Validation

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that nested components inside a subpipeline (both nested sub-agents and nested sub-pipelines) produce zero validation findings of any severity, while the parent agent's own fields are still evaluated.

**Coverage:**
- Nested sub-agent inside a subpipeline is not evaluated as a direct sub-agent of the parent
- Nested sub-pipeline inside a subpipeline is not evaluated at all
- Pipeline exclusion applies recursively — the entire pipeline tree is excluded
- Parent agent's own fields remain in the validation scope

## Preconditions

- Logged in to ELITEA as a regular user
- Environment: {{base_url}}
- Agent `TestAgent_B` has 1 direct subpipeline `ParentPipeline`
- Inside `ParentPipeline`: 1 nested sub-agent `NestedAgent` + 1 nested sub-pipeline `NestedPipeline`
- `TestAgent_B` has no direct sub-agents of its own

## Test Data

- Agent: `TestAgent_B`
- Direct subpipeline: `ParentPipeline`
- Inside `ParentPipeline`: nested sub-agent `NestedAgent`, nested sub-pipeline `NestedPipeline`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open `TestAgent_B`. Confirm `ParentPipeline` is the only attachment and there are no direct sub-agents. Click **Publish** → **Continue**. | Validation runs and completes. |
| 2 | Review all validation results across all severity levels (Critical, Warning, Info). | Zero findings of any severity reference `ParentPipeline`, `NestedAgent`, or `NestedPipeline`. At least one validation entry exists for `TestAgent_B`'s own fields (parent agent was evaluated). |

## Expected Final State

Zero findings of any severity reference `ParentPipeline`, `NestedAgent`, or `NestedPipeline`. At least one validation entry exists for `TestAgent_B`'s own fields (parent agent was evaluated).

## Pass/Fail Criteria

**Pass:**
- 0 errors/warnings/suggestions from `ParentPipeline`, `NestedAgent`, or `NestedPipeline`
- At least one validation entry for `TestAgent_B`'s own fields is present

**Fail:**
- Any finding of any severity references `NestedAgent`, `NestedPipeline`, or `ParentPipeline`
- Validation output is completely empty
