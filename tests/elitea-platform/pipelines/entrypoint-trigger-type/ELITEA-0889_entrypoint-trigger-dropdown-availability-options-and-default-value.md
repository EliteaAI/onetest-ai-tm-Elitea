---
id: ELITEA-0889
title: "Entrypoint Trigger Dropdown — Availability, Options, and Default Value"
priority: high
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [pipeline, R-2.0.3, trigger, smoke]
requirements: [EliteaAI/elitea_issues#4827]
---
# ELITEA-0889: Entrypoint Trigger Dropdown — Availability, Options, and Default Value

**Module:** Entrypoint Trigger Type · **Priority:** High · **Type:** Functional

**Objective:** Verifies that the Trigger dropdown appears exclusively on the Entrypoint node, shows the correct three options (Chat Message, Schedule, Webhook), defaults to Chat Message, and that the first node added to a pipeline is automatically set as the Entrypoint.

## Preconditions

User is logged in with pipeline edit permissions
At least one project is available
A new, empty pipeline is available for configuration (or can be created)

## Test Data

New pipeline with no nodes added yet
A second pipeline with multiple nodes where only the first node was added as the Entrypoint

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a pipeline in edit mode that has an Entrypoint node and at least one non-Entrypoint node | Pipeline canvas is displayed |
| 2 | Click on the Entrypoint node to open its configuration panel | Entrypoint node config panel opens |
| 3 | Inspect the Trigger field in the Entrypoint node config panel | A 'Trigger' dropdown is visible at the top of the node config panel, above other node config fields |
| 4 | Click on the Trigger dropdown and observe the available options | Dropdown shows exactly three options: 'Chat Message', 'Schedule', 'Webhook' — no other options are present |
| 5 | Observe the currently selected value without making any change | The default selected value is 'Chat Message' |
| 6 | Click on a non-Entrypoint node in the pipeline and inspect its config panel | No 'Trigger' field or dropdown is present on any non-Entrypoint node |
| 7 | Create a new empty pipeline and add the very first node | The first node added to the pipeline is automatically designated as the Entrypoint node |
| 8 | Inspect the auto-assigned Entrypoint node's config | Trigger dropdown is present and shows 'Chat Message' as the default |

## Expected Final State

Trigger dropdown is present and shows 'Chat Message' as the default

## Pass/Fail Criteria

PASS: Trigger dropdown present on Entrypoint node only; absent on all other nodes; exactly three options; default is Chat Message; first node auto-set as Entrypoint
FAIL: Trigger dropdown appears on a non-Entrypoint node; dropdown shows fewer/more than three options; default is anything other than Chat Message; first node is not auto-set as Entrypoint
