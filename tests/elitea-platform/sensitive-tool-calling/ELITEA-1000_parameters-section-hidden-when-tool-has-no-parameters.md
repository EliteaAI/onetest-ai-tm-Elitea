---
id: ELITEA-1000
title: "Parameters Section Hidden When Tool Has No Parameters"
priority: high
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1000: Parameters Section Hidden When Tool Has No Parameters

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a sensitive tool takes no input parameters, the "Parameters" section is not rendered in the authorization dialog.

## Preconditions

- A sensitive tool that accepts no parameters is configured (e.g., a hypothetical github > list_repositories with no inputs)
- Authorization dialog is triggered for this parameterless tool

## Test Data

- Sensitive parameterless tool scenario (e.g., github > list_repositories with no inputs)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Trigger an agent run that invokes the configured parameterless sensitive tool. | Authorization dialog appears. |
| 2 | Observe the dialog for the Parameters section. | No 'Parameters' accordion or section is rendered in the dialog. The dialog shows title, action name, policy message, and buttons — but no Parameters area. |
| 3 | Click [Authorize]. | Dialog closes. Tool executes normally despite having no parameters. |

## Expected Final State

Dialog closes. Tool executes normally despite having no parameters.

## Pass/Fail Criteria

Pass:
- Parameters section is entirely absent when the tool has no parameters
- Dialog still functions correctly (Authorize/Block work as expected)

Fail:
- An empty Parameters section is rendered (even with no key-value pairs)
- Dialog shows 'Parameters: (empty)' or similar
