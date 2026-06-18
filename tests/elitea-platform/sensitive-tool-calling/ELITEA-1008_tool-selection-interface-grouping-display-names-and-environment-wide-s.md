---
id: ELITEA-1008
title: "Tool Selection Interface — Grouping, Display Names, and Environment-Wide Scope"
priority: high
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1008: Tool Selection Interface — Grouping, Display Names, and Environment-Wide Scope

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that tools are correctly grouped by toolkit in the selection UI, each tool shows a human-readable display name (not internal ID), and the configuration applied is environment-wide (affects multiple projects).

## Preconditions

- Admin UI → Configuration → Guardrails is accessible
- Multiple projects exist (Project A and Project B) each with an agent containing the GitHub toolkit

## Test Data

- Toolkit: github
- Tool selected: create_pull_request
- Projects: Project A, Project B

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. Open the tool selection interface. | Tools are organized/grouped under their parent toolkit name (e.g., all GitHub tools under a 'GitHub' heading). |
| 2 | Expand the GitHub toolkit group. Observe individual tool entries. | Each tool shows its readable display name (e.g., 'Create Pull Request') not an internal identifier (e.g., create_pull_request). |
| 3 | Check create_pull_request. Save configuration. Restart services. | Configuration saved. |
| 4 | In Project A, open an agent with the GitHub toolkit. Trigger a prompt that invokes create_pull_request. | Authorization dialog appears in Project A. |
| 5 | In Project B, open an agent with the GitHub toolkit. Trigger the same tool. | Authorization dialog appears in Project B as well. Same configuration applies environment-wide. |

## Expected Final State

Authorization dialog appears in Project B as well. Same configuration applies environment-wide.

## Pass/Fail Criteria

Pass:
- Tools are grouped by toolkit in the UI
- Display names are human-readable (not raw internal IDs)
- The sensitive tool configuration applies across multiple projects

Fail:
- Tools are not grouped — shown as a flat list
- Only internal IDs are shown
- Configuration only affects one project; the other project has no dialog
