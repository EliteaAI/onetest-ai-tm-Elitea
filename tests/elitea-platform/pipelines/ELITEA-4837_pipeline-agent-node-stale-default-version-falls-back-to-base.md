---
id: ELITEA-4837
title: "Pipeline Agent node - stale default version falls back to the base version for the nesting check"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, feat:pipeline_nodes, feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7085]
---
# ELITEA-4837: Pipeline Agent node - stale default version falls back to the base version for the nesting check

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when an agent's `default_version_id` is missing or points to a version that no longer exists, the nesting check uses the **base** version instead of failing the list.

## Preconditions

- Logged in to {{base_url}}
- Needs dev help: two test agents in **Bugs & Features** whose default version metadata is broken (set by dev through the database or API):
  - **QA-Stale-Deep**: `default_version_id` is stale or empty, and its **base** version is 4 tiers.
  - **QA-Stale-Shallow**: `default_version_id` is stale or empty, and its **base** version is 1 tier.
- Agent **Multipurpose** (normal, valid default version)

## Test Data

| Agent | default_version_id | Base depth | Expected in Agent node |
|---|---|---|---|
| QA-Stale-Deep | stale or missing | 4 tiers | Disabled, nesting tooltip |
| QA-Stale-Shallow | stale or missing | 1 tier | Enabled |
| Multipurpose | valid | normal | Enabled |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open {{base_url}}, project **Bugs & Features**, **Explore → Pipelines**, open a pipeline and add an **Agent** node. | The Agent node panel opens. |
| 2 | Open **Agents & Pipelines**. | The list loads normally with no error toast and no empty list. Other agents (e.g. **Multipurpose**) are listed and enabled. |
| 3 | Hover over **QA-Stale-Deep**. | It's greyed out with the nesting tooltip for **QA-Stale-Deep**, because **base** is used. |
| 4 | Click **QA-Stale-Deep**. | Nothing is selected. |
| 5 | Select **QA-Stale-Shallow**. | It's enabled and selected, and **Version** shows **base**. |
| 6 | Click **Save** and reload the page. | The pipeline saves and keeps **QA-Stale-Shallow**. |

## Expected Final State

Agents with broken default version data are still listed, and their state is decided by the **base** version.

## Pass/Fail Criteria

**Pass:** Both agents are listed, the deep one is disabled and the shallow one is selectable, and the list doesn't fail.
**Fail:** The list is empty or errors, a broken agent is hidden, or the state ignores **base**.
