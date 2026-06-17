---
id: ELITEA-0670
title: "\"Forked from\" Link Accurate in Card View and Table View for Agents and Pipelines"
priority: high
type: functional
module: fork
status: ready
execution_type: manual
tags: [feat:import-forking, story:3728, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3728]
---
# ELITEA-0670: "Forked from" Link Accurate in Card View and Table View for Agents and Pipelines

**Module:** Fork · **Priority:** High · **Type:** Functional

**Objective:** Verify the "Forked from" indicator renders correctly with a working navigation link in both Card View and Table View for both Agents and Pipelines.

**Coverage:**
- "Forked from" link rendering in Card View
- "Forked from" link rendering in Table View
- Correct link destination (source project + entity)
- Coverage for both entity types: agents and pipelines

## Preconditions

- At least one agent and one pipeline already forked to Target Project
- Both forked entities have `is_forked = true`

## Test Data

- Forked agent in Target Project (any)
- Forked pipeline in Target Project (any)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Target Project → Agents → switch to Card View | Agent cards displayed |
| 2 | Locate the forked agent; verify "Forked from" link is visible on the card | Link present |
| 3 | Click the link | Navigates to the correct source agent in Source Project (correct URL) |
| 4 | Return; switch to Table View | Table rows displayed |
| 5 | Locate the forked agent row; verify "Forked from" link is visible | Link present in the row |
| 6 | Click the link | Same correct navigation to source agent |
| 7 | Target Project → Pipelines → Card View | Pipeline cards displayed |
| 8 | Locate the forked pipeline; verify "Forked from" link visible | Link present |
| 9 | Click the link | Navigates to correct source pipeline in Source Project |
| 10 | Switch to Table View for Pipelines; verify link present and correct | Link present and functional |

## Expected Final State

Link present and functional

## Pass/Fail Criteria

**Pass:**
- "Forked from" link visible and accurate in all four combinations (agent/pipeline × card/table)

**Fail:**
- Link absent for pipeline entities (indicating is_forked not set for pipelines)
- Link present but navigates to wrong entity or project
- Link present in Card View but absent in Table View or vice versa
