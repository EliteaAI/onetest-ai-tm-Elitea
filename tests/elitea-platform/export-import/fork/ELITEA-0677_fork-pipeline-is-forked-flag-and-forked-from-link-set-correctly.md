---
id: ELITEA-0677
title: "Fork Pipeline — is_forked Flag and \"Forked from\" Link Set Correctly"
priority: critical
type: functional
module: fork
status: ready
execution_type: manual
tags: [feat:import-forking, story:3728, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3728]
---
# ELITEA-0677: Fork Pipeline — is_forked Flag and "Forked from" Link Set Correctly

**Module:** Fork · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that forking a Pipeline entity sets `is_forked = true` and displays a "Forked from" link, confirming the v2 fork backend processes pipeline entity type correctly.

**Coverage:**
- Pipeline fork metadata injection (`is_forked` for pipeline entity type)
- "Forked from" link for pipelines in both Card View and Table View
- Version isolation for pipelines

## Preconditions

- Logged in as Editor in Source Project and Target Project
- Source Project has at least one Pipeline with multiple versions

## Test Data

- Source pipeline: any pipeline with ≥2 versions
- Active version during fork: non-latest version
- Target Project: different from Source Project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines in Source Project → open a pipeline → switch to a non-latest version | Pipeline detail shows selected version |
| 2 | Click Fork (icon or ... menu) | Fork wizard opens with title "Fork parameters" |
| 3 | Select Target Project → click Fork | Wizard completes, "Fork Complete" shown |
| 4 | Navigate to Target Project → Pipelines → locate the forked pipeline | Forked pipeline is present |
| 5 | Switch to Card View — check for "Forked from" indicator | "Forked from" link is visible on the card |
| 6 | Switch to Table View — check for "Forked from" indicator | "Forked from" link is visible in the table row |
| 7 | Click the "Forked from" link | Navigates to the original pipeline in Source Project |
| 8 | Open the forked pipeline and inspect versions | Only the version active at fork time is present |

## Expected Final State

Only the version active at fork time is present

## Pass/Fail Criteria

**Pass:**
- "Forked from" link visible in both Card View and Table View for the pipeline
- Link navigates correctly to the source pipeline
- Only the forked version is present

**Fail:**
- "Forked from" link is absent for the pipeline (indicating `is_forked` was not set)
- All versions copied instead of only the active one
- Wizard errors during pipeline fork
